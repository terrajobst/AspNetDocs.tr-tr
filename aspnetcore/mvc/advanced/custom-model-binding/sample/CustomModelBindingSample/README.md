---
ms.openlocfilehash: 71a40fcab8f1d1005cbe9327d01a42484765a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076554"
---
# <a name="custom-model-binding-demo"></a>Özel Model bağlama Tanıtımı

Test `ByteArrayModelBinder` uygulamayı çalıştırarak ve base64 ile kodlanmış dizeye yayınlayarak `ImageController` uç noktası (`/api/image/`). İstek gövdesini form verileri olarak dosya ve dosya özelliklerini belirtin (kullanarak [Postman](https://www.getpostman.com/) veya benzer bir araç). Kullanabileceğiniz [Bu örnek dizedir](Base64String.txt). Sonuç kaydedilir *wwwroot/resimler/karşıya yüklediğiniz* klasör belirtilen dosya adına sahip.

Özel bağlama örnek test etmek için aşağıdaki uç noktaların deneyin:

* /api/Authors/1
* /api/Authors/2 (bulunamadı)
* /api/boundauthors/1
* /api/boundauthors/2 (bulunamadı)
* /api/boundauthors/Get/1
* (içerik yok) /api/boundauthors/Get/2 &ndash; Bu eylem için null denetlemez ve döndüren bir *404 Bulunamadı*.
