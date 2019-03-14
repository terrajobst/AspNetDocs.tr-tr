---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073110"
---

> [!NOTE]
> <span data-ttu-id="b4270-101">Birçok şema değiştirme işlemlerini EF Core SQLite sağlayıcı tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b4270-101">Many schema change operations are not supported by the EF Core SQLite provider.</span></span> <span data-ttu-id="b4270-102">Örneğin, sütun ekleme desteklenir, ancak bir sütun kaldırılması desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b4270-102">For example, adding a column is supported, but removing a column is not supported.</span></span> <span data-ttu-id="b4270-103">Bir sütunu kaldırmak için bir geçiş oluşturduysanız `ef migrations add` komut başarılı ancak `ef database update` komutu başarısız oluyor.</span><span class="sxs-lookup"><span data-stu-id="b4270-103">If a migration is created to remove a column, the `ef migrations add` command succeeds but the `ef database update` command fails.</span></span> <span data-ttu-id="b4270-104">Bu sınırlamaların bazıları el ile bir tablo yeniden oluşturma gerçekleştirmek için geçişler kod yazarak üstesinden.</span><span class="sxs-lookup"><span data-stu-id="b4270-104">Some of these limitations can be overcome by manually writing migrations code to perform a table rebuild.</span></span> <span data-ttu-id="b4270-105">Bir tablo yeniden oluşturma içerir:</span><span class="sxs-lookup"><span data-stu-id="b4270-105">A table rebuild involves:</span></span>

>* <span data-ttu-id="b4270-106">Varolan bir tabloyu yeniden adlandırma.</span><span class="sxs-lookup"><span data-stu-id="b4270-106">Renaming the existing table.</span></span>
>* <span data-ttu-id="b4270-107">Yeni bir tablo oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="b4270-107">Creating a new table.</span></span>
>* <span data-ttu-id="b4270-108">Verileri yeni tabloya eski tablodan kopyalama.</span><span class="sxs-lookup"><span data-stu-id="b4270-108">Copying data from the old table to the new table.</span></span>
>* <span data-ttu-id="b4270-109">Eski tablosu bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="b4270-109">Dropping the old table.</span></span>

<span data-ttu-id="b4270-110">Daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="b4270-110">For more information, see the following resources:</span></span>
> * [<span data-ttu-id="b4270-111">SQLite EF Core veritabanı sağlayıcısı sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="b4270-111">SQLite EF Core Database Provider Limitations</span></span>](/ef/core/providers/sqlite/limitations)
> * [<span data-ttu-id="b4270-112">Geçiş kodu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="b4270-112">Customize migration code</span></span>](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [<span data-ttu-id="b4270-113">Veri çekirdeği oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4270-113">Data seeding</span></span>](/ef/core/modeling/data-seeding)