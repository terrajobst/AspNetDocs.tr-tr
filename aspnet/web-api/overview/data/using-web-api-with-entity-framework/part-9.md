---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: Veritabanına yeni öğe ekleme | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 01586ef6eecdbe1acfadfcfcc0c9ca8b442de2d3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072153"
---
<a name="add-a-new-item-to-the-database"></a>Veritabanına Yeni Öğe Ekleme
====================
tarafından [Mike Wasson](https://github.com/MikeWasson)

[Projeyi yükle](https://github.com/MikeWasson/BookService)

Bu bölümde, kullanıcıların yeni kitabı oluşturmasını özelliği ekler. App.js içinde görünüm modeli için aşağıdaki kodu ekleyin:

[!code-javascript[Main](part-9/samples/sample1.js)]

Index.cshtml içinde aşağıdaki biçimlendirme değiştirin:

[!code-html[Main](part-9/samples/sample2.html)]

İle:

[!code-html[Main](part-9/samples/sample3.html)]

Bu işaretleme, yeni bir yazar göndermek için bir form oluşturur. Yazar aşağı açılan liste değerlerini verilere için bağlı `authors` gözlemlenebilir görünüm modeli. Diğer form girişler için değerleri verilere için bağlı `newBook` özelliği görünüm modeli.

Form üzerinde gönderme işleyicisi bağlı `addBook` işlevi:

[!code-html[Main](part-9/samples/sample4.html)]

`addBook` İşlevi, geçerli bir JSON nesnesi oluşturmak için verilere bağlı form girişleri değerlerini okur. JSON nesnesine gönderir sonra `/api/books`.

> [!div class="step-by-step"]
> [Önceki](part-8.md)
> [İleri](part-10.md)
