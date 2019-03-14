---
title: ASP.NET core'da basit yetkilendirme
author: rick-anderson
description: Authorize özniteliği için ASP.NET Core denetleyicilere ve eylemlere erişimi kısıtlamak için kullanmayı öğrenin.
ms.author: riande
ms.date: 10/14/2016
uid: security/authorization/simple
ms.openlocfilehash: 6409def0508b855d3d2a4a1f4d3a3d15bfe5dd32
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073848"
---
# <a name="simple-authorization-in-aspnet-core"></a>ASP.NET core'da basit yetkilendirme

<a name="security-authorization-simple"></a>

Yetkilendirme mvc'de aracılığıyla denetlenebilir `AuthorizeAttribute` özniteliği ve çeşitli parametreleri. En basit şekliyle, uygulama `AuthorizeAttribute` denetleyici veya eylem erişimi denetleyiciye veya eylem kimliği doğrulanan kullanıcı için özniteliği.

Örneğin, aşağıdaki kod erişimi sınırlar `AccountController` herhangi bir kimliği doğrulanmış kullanıcı için.

```csharp
[Authorize]
public class AccountController : Controller
{
    public ActionResult Login()
    {
    }

    public ActionResult Logout()
    {
    }
}
```

Yetkilendirme denetleyicisi yerine bir eylemi uygulamak istiyorsanız, geçerli `AuthorizeAttribute` özniteliği eylem için:

```csharp
public class AccountController : Controller
{
   public ActionResult Login()
   {
   }

   [Authorize]
   public ActionResult Logout()
   {
   }
}
```

Yalnızca kimliği doğrulanmış kullanıcıların artık `Logout` işlevi.

Ayrıca `AllowAnonymous` bireysel işlemlere doğrulanmamış kullanıcılar tarafından erişime izin vermek için özniteliği. Örneğin:

```csharp
[Authorize]
public class AccountController : Controller
{
    [AllowAnonymous]
    public ActionResult Login()
    {
    }

    public ActionResult Logout()
    {
    }
}
```

Bu yalnızca kimliği doğrulanmış kullanıcılara izin `AccountController`, dışında `Login` kimliği doğrulanmış veya kimliği doğrulanmamış / anonim durumlarını bağımsız olarak herkes tarafından erişilebilir olan bir eylem.

> [!WARNING]
> `[AllowAnonymous]` Tüm Yetkilendirme deyimleri atlar. Birleştirirseniz `[AllowAnonymous]` ve tüm `[Authorize]` özniteliği `[Authorize]` öznitelikleri yoksayılır. Örneğin, uygulamanızı `[AllowAnonymous]` denetleyici düzeyinde herhangi `[Authorize]` öznitelikleri aynı denetleyicisine (veya içindeki herhangi bir eylem) göz ardı edilir.
