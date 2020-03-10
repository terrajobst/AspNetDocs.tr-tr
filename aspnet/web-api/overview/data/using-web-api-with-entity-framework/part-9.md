---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: Veritabanına yeni bir öğe Ekle | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557290"
---
# <a name="add-a-new-item-to-the-database"></a>Veritabanına Yeni Öğe Ekleme

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://github.com/MikeWasson/BookService)

Bu bölümde, kullanıcıların yeni bir kitap oluşturmasını sağlayacak bir özellik ekleyeceksiniz. App. js ' de, görünüm modeline aşağıdaki kodu ekleyin:

[!code-javascript[Main](part-9/samples/sample1.js)]

Index. cshtml dosyasında aşağıdaki biçimlendirmeyi değiştirin:

[!code-html[Main](part-9/samples/sample2.html)]

Yerine konan:

[!code-html[Main](part-9/samples/sample3.html)]

Bu biçimlendirme yeni bir yazar göndermek için bir form oluşturur. Yazar açılan listesinin değerleri, görünüm modelinde `authors` observable 'a veri bağlalardır. Diğer form girişleri için değerler, görünüm modelinin `newBook` özelliğine veri bağımlıdır.

Formdaki gönderme işleyicisi `addBook` işlevine bağlıdır:

[!code-html[Main](part-9/samples/sample4.html)]

`addBook` işlevi, JSON nesnesi oluşturmak için veri bağlantılı form girişlerinin geçerli değerlerini okur. Ardından JSON nesnesini `/api/books`' e gönderir.

> [!div class="step-by-step"]
> [Önceki](part-8.md)
> [İleri](part-10.md)
