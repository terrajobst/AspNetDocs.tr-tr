---
ms.openlocfilehash: 4d6b6309e6e15c364542b5d3ae296d53c6ea4358
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069840"
---
<span data-ttu-id="9a9c4-101">Oluşturulan kimlik veritabanı kod gerektirir [Entity Framework Code Migrations](/ef/core/managing-schemas/migrations/).</span><span class="sxs-lookup"><span data-stu-id="9a9c4-101">The generated Identity database code requires [Entity Framework Core Migrations](/ef/core/managing-schemas/migrations/).</span></span> <span data-ttu-id="9a9c4-102">Bir geçiş oluşturmak ve veritabanı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9a9c4-102">Create a migration and update the database.</span></span> <span data-ttu-id="9a9c4-103">Örneğin, aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9a9c4-103">For example, run the following commands:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="9a9c4-104">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9a9c4-104">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="9a9c4-105">Visual Studio **Paket Yöneticisi Konsolu**:</span><span class="sxs-lookup"><span data-stu-id="9a9c4-105">In the Visual Studio **Package Manager Console**:</span></span>

```PMC
Add-Migration CreateIdentitySchema
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="9a9c4-106">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="9a9c4-106">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
```

------

<span data-ttu-id="9a9c4-107">"CreateIdentitySchema" name parametresi için `Add-Migration` rastgele komutu.</span><span class="sxs-lookup"><span data-stu-id="9a9c4-107">The "CreateIdentitySchema" name parameter for the `Add-Migration` command is arbitrary.</span></span> <span data-ttu-id="9a9c4-108">`"CreateIdentitySchema"` geçiş açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="9a9c4-108">`"CreateIdentitySchema"` describes the migration.</span></span>
