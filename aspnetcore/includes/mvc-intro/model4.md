---
ms.openlocfilehash: 568fa161b27e554fd8b474670b8f9a7ec2f39f45
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072783"
---
<span data-ttu-id="ffb61-101">Aşağıdaki tabloda, ASP.NET Core Kod Oluşturucu parametreleri ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="ffb61-101">The following table details the ASP.NET Core code generator parameters:</span></span>

| <span data-ttu-id="ffb61-102">Parametre</span><span class="sxs-lookup"><span data-stu-id="ffb61-102">Parameter</span></span>               | <span data-ttu-id="ffb61-103">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ffb61-103">Description</span></span>|
| ----------------- | ------------ |
| <span data-ttu-id="ffb61-104">-m</span><span class="sxs-lookup"><span data-stu-id="ffb61-104">-m</span></span>  | <span data-ttu-id="ffb61-105">Modelin adı.</span><span class="sxs-lookup"><span data-stu-id="ffb61-105">The name of the model.</span></span> |
| <span data-ttu-id="ffb61-106">-dc</span><span class="sxs-lookup"><span data-stu-id="ffb61-106">-dc</span></span>  | <span data-ttu-id="ffb61-107">Veri bağlamı.</span><span class="sxs-lookup"><span data-stu-id="ffb61-107">The data context.</span></span> |
| <span data-ttu-id="ffb61-108">-udl</span><span class="sxs-lookup"><span data-stu-id="ffb61-108">-udl</span></span> | <span data-ttu-id="ffb61-109">Ekran düzenini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ffb61-109">Use the default layout.</span></span> |
| <span data-ttu-id="ffb61-110">--relativeFolderPath</span><span class="sxs-lookup"><span data-stu-id="ffb61-110">--relativeFolderPath</span></span> | <span data-ttu-id="ffb61-111">Görünümleri oluşturmak için göreli çıkış klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="ffb61-111">The relative output folder path to create the views.</span></span> |
| <span data-ttu-id="ffb61-112">--useDefaultLayout</span><span class="sxs-lookup"><span data-stu-id="ffb61-112">--useDefaultLayout</span></span> | <span data-ttu-id="ffb61-113">Varsayılan düzen görünümleri için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ffb61-113">The default layout should be used for the views.</span></span> |
| <span data-ttu-id="ffb61-114">--referenceScriptLibraries</span><span class="sxs-lookup"><span data-stu-id="ffb61-114">--referenceScriptLibraries</span></span> | <span data-ttu-id="ffb61-115">Ekler `_ValidationScriptsPartial` düzenleyip sayfaları oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="ffb61-115">Adds `_ValidationScriptsPartial` to Edit and Create pages</span></span> |

<span data-ttu-id="ffb61-116">Kullanım `h` hakkında Yardım almak için anahtar `aspnet-codegenerator controller` komutu:</span><span class="sxs-lookup"><span data-stu-id="ffb61-116">Use the `h` switch to get help on the `aspnet-codegenerator controller` command:</span></span>

```console
dotnet aspnet-codegenerator controller -h
```