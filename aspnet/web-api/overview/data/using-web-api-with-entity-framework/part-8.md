---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: Öğe ayrıntılarını görüntüleme | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59389056"
---
# <a name="display-item-details"></a>Öğe Ayrıntılarını Görüntüleme

tarafından [Mike Wasson](https://github.com/MikeWasson)

[Projeyi yükle](https://github.com/MikeWasson/BookService)

Bu bölümde, her bir kitabın ayrıntılarını görüntülemek için özelliğini ekleyecektir. App.js içinde görünüm modeli aşağıdaki kodu ekleyin:

[!code-javascript[Main](part-8/samples/sample1.js)]

Views/Home/Index.cshtml içinde veri bağlama öğesi ayrıntıları bağlantısını ekleyin:

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

Bu tıklama işleyicisine bağlar &lt;bir&gt; öğesine `getBookDetail` işlevi bir görünüm modeli.

Aynı dosyada, aşağıdaki işaretleme değiştirin:

[!code-html[Main](part-8/samples/sample3.html)]

şununla değiştirin:

[!code-html[Main](part-8/samples/sample4.html)]

Bu işaretleme, veri özelliklerine bağlı bir tablo oluşturur `detail` gözlemlenebilir görünüm modeli.

"&lt;!--Ko--&gt; &quot; DOM öğesinin dışında Knockout bağlama dahil söz dizimi sağlar. Bu durumda, `if` bağlama neden olur, bu bölümde görüntülenecek biçimlendirme yalnızca `details` null değil.

[!code-html[Main](part-8/samples/sample5.html)]

Şimdi uygulamayı çalıştırabilir ve birine tıklayın &quot;ayrıntı&quot; bağlantıları, uygulama kitap ayrıntılarını görüntüler.

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> [Önceki](part-7.md)
> [İleri](part-9.md)
