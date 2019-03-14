---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073110"
---

> [!NOTE]
> Birçok şema değiştirme işlemlerini EF Core SQLite sağlayıcı tarafından desteklenmiyor. Örneğin, sütun ekleme desteklenir, ancak bir sütun kaldırılması desteklenmiyor. Bir sütunu kaldırmak için bir geçiş oluşturduysanız `ef migrations add` komut başarılı ancak `ef database update` komutu başarısız oluyor. Bu sınırlamaların bazıları el ile bir tablo yeniden oluşturma gerçekleştirmek için geçişler kod yazarak üstesinden. Bir tablo yeniden oluşturma içerir:

>* Varolan bir tabloyu yeniden adlandırma.
>* Yeni bir tablo oluşturuluyor.
>* Verileri yeni tabloya eski tablodan kopyalama.
>* Eski tablosu bırakılıyor.

Daha fazla bilgi için aşağıdaki kaynaklara bakın:
> * [SQLite EF Core veritabanı sağlayıcısı sınırlamaları](/ef/core/providers/sqlite/limitations)
> * [Geçiş kodu özelleştirme](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [Veri çekirdeği oluşturma](/ef/core/modeling/data-seeding)