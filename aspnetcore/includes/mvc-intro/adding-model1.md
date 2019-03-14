---
ms.openlocfilehash: 72e33ea44976963193d2560427fc418875be450e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070293"
---
# <a name="add-a-model-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="b238a-101">Bir ASP.NET Core MVC uygulaması için bir model ekleme</span><span class="sxs-lookup"><span data-stu-id="b238a-101">Add a model to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="b238a-102">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT) ve [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="b238a-102">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="b238a-103">Bu bölümde, bir veritabanında filmler yönetmek için bazı sınıflar ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b238a-103">In this section, you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="b238a-104">Bu sınıflar olacaktır "**M**odel" parçası **M**VC uygulama.</span><span class="sxs-lookup"><span data-stu-id="b238a-104">These classes will be the "**M**odel" part of the **M**VC app.</span></span>

<span data-ttu-id="b238a-105">Bu sınıflar ile kullandığınız [Entity Framework Core](/ef/core) bir veritabanıyla çalışmak için (EF Core).</span><span class="sxs-lookup"><span data-stu-id="b238a-105">You use these classes with [Entity Framework Core](/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="b238a-106">EF Core, yazmanız gereken veri erişim kodu kolaylaştıran bir nesne ilişkisel eşleme (ORM) çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="b238a-106">EF Core is an object-relational mapping (ORM) framework that simplifies the data access code that you have to write.</span></span> <span data-ttu-id="b238a-107">[EF Core birçok veritabanı altyapılarını destekleyen](/ef/core/providers/).</span><span class="sxs-lookup"><span data-stu-id="b238a-107">[EF Core supports many database engines](/ef/core/providers/).</span></span>

<span data-ttu-id="b238a-108">EF Core üzerinde herhangi bir bağımlılığı olmadığından oluşturacağınız model sınıfları ("düz eski CLR nesnelerden") POCO sınıfları olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="b238a-108">The model classes you'll create are known as POCO classes (from "plain-old CLR objects") because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="b238a-109">Bunlar yalnızca veritabanında depolanan verilerin özelliklerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b238a-109">They just define the properties of the data that will be stored in the database.</span></span>

<span data-ttu-id="b238a-110">Bu öğreticide, model sınıfları ilk yazacaksınız ve EF Core veritabanı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b238a-110">In this tutorial you'll write the model classes first, and EF Core will create the database.</span></span> <span data-ttu-id="b238a-111">Burada ele alınmamaktadır alternatif bir yaklaşım, model sınıfları zaten varolan bir veritabanı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="b238a-111">An alternate approach not covered here is to generate model classes from an already-existing database.</span></span> <span data-ttu-id="b238a-112">Bu yaklaşımı hakkında daha fazla bilgi için bkz. [ASP.NET Core - mevcut veritabanı](/ef/core/get-started/aspnetcore/existing-db).</span><span class="sxs-lookup"><span data-stu-id="b238a-112">For information about that approach, see [ASP.NET Core - Existing Database](/ef/core/get-started/aspnetcore/existing-db).</span></span>

## <a name="add-a-data-model-class"></a><span data-ttu-id="b238a-113">Bir veri modeli sınıfı Ekle</span><span class="sxs-lookup"><span data-stu-id="b238a-113">Add a data model class</span></span>
