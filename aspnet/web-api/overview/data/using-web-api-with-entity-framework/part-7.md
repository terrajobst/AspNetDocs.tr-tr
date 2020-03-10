---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: Görünüm oluşturma (UI) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 62c4523c2c6fb399cfbc3716309a1379996d601c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557304"
---
# <a name="create-the-view-ui"></a>Görünümü (Kullanıcı Arabirimi) Oluşturma

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://github.com/MikeWasson/BookService)

Bu bölümde, uygulamanın HTML 'sini tanımlamaya ve HTML ile görünüm modeli arasında veri bağlama eklemeye başlayacaksınız.

Views/Home/Index. cshtml dosyasını açın. Bu dosyanın tüm içeriğini aşağıdaki kodla değiştirin.

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

`div` öğelerinin çoğu [önyükleme](http://getbootstrap.com/) stili için vardır. Önemli öğeler `data-bind` öznitelikleridir. Bu öznitelik HTML 'i görünüm modeline bağlar.

Örneğin:

[!code-html[Main](part-7/samples/sample2.html)]

Bu örnekte, &quot;`text`&quot; bağlama `<p>` öğenin görünüm modelinden `error` özelliğinin değerini göstermesini sağlar. `error` `ko.observable`olarak bildirildiği hatırlayın:

[!code-javascript[Main](part-7/samples/sample3.js)]

`error`için yeni bir değer atandığında, altını Gizle `<p>` öğesindeki metni günceller.

`foreach` bağlama, altını gizlemeyi `books` dizisinin içerikleri aracılığıyla döngüye bildirir. Dizideki her öğe için, altını gizleme yeni bir &lt;li&gt; öğesi oluşturur. `foreach` bağlamı içindeki bağlamalar, dizi öğesindeki özelliklere başvurur. Örneğin:

[!code-html[Main](part-7/samples/sample4.html)]

Burada `text` bağlama her kitabın Author özelliğini okur.

Uygulamayı şimdi çalıştırırsanız, şöyle görünmelidir:

![](part-7/_static/image1.png)

Kitaplar Listesi, sayfa yüklendikten sonra zaman uyumsuz olarak yüklenir. Şu anda &quot;ayrıntıları&quot; bağlantılar işlevsel değildir. Sonraki bölümde bu işlevselliği ekleyeceğiz.

> [!div class="step-by-step"]
> [Önceki](part-6.md)
> [İleri](part-8.md)
