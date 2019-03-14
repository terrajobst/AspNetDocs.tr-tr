---
ms.openlocfilehash: 1c342231905775938715280681ea2b4cf6ebc9bc
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073026"
---
Aşağıdaki özellikleri `Movie` sınıfı:

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Models/Movie.cs?name=snippet1)]

`Movie` Sınıfı içerir:

* `Id` Alanı ve veritabanı için birincil anahtarı gereklidir.
* `[DataType(DataType.Date)]`:  [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) özniteliği veri türünü belirtir (`Date`). Bu öznitelik ile:

  * Kullanıcının tarih alanı saat bilgilerini girmek için gerekli değildir.
  * Yalnızca tarih görüntülenen, olmayan zaman bilgilerdir.

[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) bir sonraki öğreticide ele alınmaktadır.