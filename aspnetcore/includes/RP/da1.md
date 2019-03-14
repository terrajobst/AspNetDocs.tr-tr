---
ms.openlocfilehash: e5565381f44480e2531925717ee7815da92d1ff5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067626"
---
# <a name="update-the-generated-pages"></a><span data-ttu-id="e4d90-101">Oluşturulan sayfaları güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e4d90-101">Update the generated pages</span></span>

<span data-ttu-id="e4d90-102">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="e4d90-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="e4d90-103">Film uygulaması için iyi bir başlangıç sahibiz ancak sunu ideal değildir.</span><span class="sxs-lookup"><span data-stu-id="e4d90-103">We have a good start to the movie app, but the presentation isn't ideal.</span></span> <span data-ttu-id="e4d90-104">Saat (12:00: 00'da aşağıdaki görüntüde) görmesini istemediğiniz ve **ReleaseDate** olmalıdır **yayın tarihi** (iki kelimeye).</span><span class="sxs-lookup"><span data-stu-id="e4d90-104">We don't want to see the time (12:00:00 AM in the image below) and **ReleaseDate** should be **Release Date** (two words).</span></span>

![Film verileri gösteren Chrome'da açık film uygulaması](../../tutorials/razor-pages/sql/_static/m55.png)

## <a name="update-the-generated-code"></a><span data-ttu-id="e4d90-106">Oluşturulan kodu güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e4d90-106">Update the generated code</span></span>

<span data-ttu-id="e4d90-107">Açık *Models/Movie.cs* dosya ve aşağıdaki kodda gösterilen vurgulanan satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e4d90-107">Open the *Models/Movie.cs* file and add the highlighted lines shown in the following code:</span></span>

[!code-csharp[](code/Models/Movie.cs?highlight=2,11-12)]
