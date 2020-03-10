---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: Öğe ayrıntılarını görüntüle | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557325"
---
# <a name="display-item-details"></a>Öğe Ayrıntılarını Görüntüleme

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://github.com/MikeWasson/BookService)

Bu bölümde, her bir kitabın ayrıntılarını görüntüleme özelliğini ekleyeceksiniz. App. js ' de, görünüm modeline aşağıdaki koda ekleyin:

[!code-javascript[Main](part-8/samples/sample1.js)]

Görünümler/Home/Index. cshtml 'de, Ayrıntılar bağlantısına bir veri bağlama öğesi ekleyin:

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

Bu, bir&gt; öğesi &lt;için tıklama işleyicisini görünüm modelindeki `getBookDetail` işlevine bağlar.

Aynı dosyada, aşağıdaki işareti değiştirin:

[!code-html[Main](part-8/samples/sample3.html)]

şununla değiştirin:

[!code-html[Main](part-8/samples/sample4.html)]

Bu biçimlendirme, görünüm modelinde `detail` observable özelliklerine veri bağlanan bir tablo oluşturur.

"&lt;!--Ko--&gt;&quot; sözdizimi, DOM öğesinin dışında bir altını gizleme bağlamayı eklemenize olanak tanır. Bu durumda `if` bağlama, biçimlendirmenin bu bölümünün yalnızca `details` null olmadığı durumlarda görüntülenmesine neden olur.

[!code-html[Main](part-8/samples/sample5.html)]

Uygulamayı çalıştırıp &quot;ayrıntılarından birine&quot; bağlantılardan birine tıklarsanız, uygulama kitap ayrıntılarını görüntüler.

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> [Önceki](part-7.md)
> [İleri](part-9.md)
