---
ms.openlocfilehash: 71a40fcab8f1d1005cbe9327d01a42484765a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076554"
---
# <a name="custom-model-binding-demo"></a><span data-ttu-id="67714-101">Özel Model bağlama Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="67714-101">Custom Model Binding Demo</span></span>

<span data-ttu-id="67714-102">Test `ByteArrayModelBinder` uygulamayı çalıştırarak ve base64 ile kodlanmış dizeye yayınlayarak `ImageController` uç noktası (`/api/image/`).</span><span class="sxs-lookup"><span data-stu-id="67714-102">Test `ByteArrayModelBinder` by running the app and POSTing a base64-encoded string to the `ImageController` endpoint (`/api/image/`).</span></span> <span data-ttu-id="67714-103">İstek gövdesini form verileri olarak dosya ve dosya özelliklerini belirtin (kullanarak [Postman](https://www.getpostman.com/) veya benzer bir araç).</span><span class="sxs-lookup"><span data-stu-id="67714-103">Specify the file and filename properties in the request body as form-data (using [Postman](https://www.getpostman.com/) or a similar tool).</span></span> <span data-ttu-id="67714-104">Kullanabileceğiniz [Bu örnek dizedir](Base64String.txt).</span><span class="sxs-lookup"><span data-stu-id="67714-104">You can use [this sample string](Base64String.txt).</span></span> <span data-ttu-id="67714-105">Sonuç kaydedilir *wwwroot/resimler/karşıya yüklediğiniz* klasör belirtilen dosya adına sahip.</span><span class="sxs-lookup"><span data-stu-id="67714-105">The result is saved in the *wwwroot/images/upload* folder with the filename specified.</span></span>

<span data-ttu-id="67714-106">Özel bağlama örnek test etmek için aşağıdaki uç noktaların deneyin:</span><span class="sxs-lookup"><span data-stu-id="67714-106">To test the custom binding example, try the following endpoints:</span></span>

* <span data-ttu-id="67714-107">/api/Authors/1</span><span class="sxs-lookup"><span data-stu-id="67714-107">/api/authors/1</span></span>
* <span data-ttu-id="67714-108">/api/Authors/2 (bulunamadı)</span><span class="sxs-lookup"><span data-stu-id="67714-108">/api/authors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="67714-109">/api/boundauthors/1</span><span class="sxs-lookup"><span data-stu-id="67714-109">/api/boundauthors/1</span></span>
* <span data-ttu-id="67714-110">/api/boundauthors/2 (bulunamadı)</span><span class="sxs-lookup"><span data-stu-id="67714-110">/api/boundauthors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="67714-111">/api/boundauthors/Get/1</span><span class="sxs-lookup"><span data-stu-id="67714-111">/api/boundauthors/get/1</span></span>
* <span data-ttu-id="67714-112">(içerik yok) /api/boundauthors/Get/2 &ndash; Bu eylem için null denetlemez ve döndüren bir *404 Bulunamadı*.</span><span class="sxs-lookup"><span data-stu-id="67714-112">/api/boundauthors/get/2 (NO CONTENT) &ndash; This action doesn't check for null and returns a *404 Not Found*.</span></span>
