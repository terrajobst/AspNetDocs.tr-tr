---
ms.openlocfilehash: 934db70fe49ba9a5330b25596dc694e0ac50c04e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069996"
---
<span data-ttu-id="a50e1-101">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a50e1-101">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="a50e1-102">Bu bölümde, bir veritabanında filmler yönetmek için sınıflar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a50e1-102">In this section, you add classes for managing movies in a database.</span></span> <span data-ttu-id="a50e1-103">Bu sınıflar ile kullandığınız [Entity Framework Core](/ef/core) bir veritabanıyla çalışmak için (EF Core).</span><span class="sxs-lookup"><span data-stu-id="a50e1-103">You use these classes with [Entity Framework Core](/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="a50e1-104">EF Core, yazmanız gereken veri erişim kodu kolaylaştıran bir nesne ilişkisel eşleme (ORM) çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="a50e1-104">EF Core is an object-relational mapping (ORM) framework that simplifies the data access code that you have to write.</span></span>

<span data-ttu-id="a50e1-105">EF Core üzerinde herhangi bir bağımlılığı olmadığından oluşturduğunuz modeli sınıfları ("düz eski CLR nesnelerden") POCO sınıfları olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="a50e1-105">The model classes you create are known as POCO classes (from "plain-old CLR objects") because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="a50e1-106">Bunlar, veritabanında depolanan verilerin özelliklerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="a50e1-106">They define the properties of the data that are stored in the database.</span></span>

<span data-ttu-id="a50e1-107">Bu öğreticide model sınıfları ilk yazma ve EF Core veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a50e1-107">In this tutorial, you write the model classes first, and EF Core creates the database.</span></span> <span data-ttu-id="a50e1-108">Burada ele alınmamaktadır alternatif bir yaklaşım [varolan bir veritabanından model sınıfları oluşturma](/ef/core/get-started/aspnetcore/existing-db).</span><span class="sxs-lookup"><span data-stu-id="a50e1-108">An alternate approach not covered here is to [generate model classes from an existing database](/ef/core/get-started/aspnetcore/existing-db).</span></span>

<span data-ttu-id="a50e1-109">[Görüntüleme veya indirme](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) örnek.</span><span class="sxs-lookup"><span data-stu-id="a50e1-109">[View or download](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) sample.</span></span>
