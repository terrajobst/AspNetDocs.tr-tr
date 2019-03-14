---
ms.openlocfilehash: 545448e3673b02abc7e685bd987f2cf5f71375b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57074238"
---
> [!WARNING]
> <span data-ttu-id="fa6d5-101">Güvenlik nedenleriyle, bağlama kabul gerekir `GET` sayfa modeli özellikleri veri isteği.</span><span class="sxs-lookup"><span data-stu-id="fa6d5-101">For security reasons, you must opt in to binding `GET` request data to page model properties.</span></span> <span data-ttu-id="fa6d5-102">Özellikleri için eşleme önce kullanıcı girişi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fa6d5-102">Verify user input before mapping it to properties.</span></span> <span data-ttu-id="fa6d5-103">İçin kabul `GET` bağlama, sorgu dizesi veya rota değerlerini senaryolarda belirtirken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="fa6d5-103">Opting in to `GET` binding is useful when addressing scenarios which rely on query string or route values.</span></span>
>
> <span data-ttu-id="fa6d5-104">Bir özelliği bağlamak `GET` istekleri, ayarlar [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) özniteliğin `SupportsGet` özelliğini `true`: `[BindProperty(SupportsGet = true)]`</span><span class="sxs-lookup"><span data-stu-id="fa6d5-104">To bind a property on `GET` requests, set the [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) attribute's `SupportsGet` property to `true`: `[BindProperty(SupportsGet = true)]`</span></span>
