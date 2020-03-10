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
# <a name="add-a-new-item-to-the-database"></a><span data-ttu-id="cbff8-102">Veritabanına Yeni Öğe Ekleme</span><span class="sxs-lookup"><span data-stu-id="cbff8-102">Add a New Item to the Database</span></span>

<span data-ttu-id="cbff8-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="cbff8-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="cbff8-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="cbff8-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="cbff8-105">Bu bölümde, kullanıcıların yeni bir kitap oluşturmasını sağlayacak bir özellik ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="cbff8-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="cbff8-106">App. js ' de, görünüm modeline aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cbff8-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="cbff8-107">Index. cshtml dosyasında aşağıdaki biçimlendirmeyi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="cbff8-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="cbff8-108">Yerine konan:</span><span class="sxs-lookup"><span data-stu-id="cbff8-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="cbff8-109">Bu biçimlendirme yeni bir yazar göndermek için bir form oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cbff8-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="cbff8-110">Yazar açılan listesinin değerleri, görünüm modelinde `authors` observable 'a veri bağlalardır.</span><span class="sxs-lookup"><span data-stu-id="cbff8-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="cbff8-111">Diğer form girişleri için değerler, görünüm modelinin `newBook` özelliğine veri bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="cbff8-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="cbff8-112">Formdaki gönderme işleyicisi `addBook` işlevine bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="cbff8-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="cbff8-113">`addBook` işlevi, JSON nesnesi oluşturmak için veri bağlantılı form girişlerinin geçerli değerlerini okur.</span><span class="sxs-lookup"><span data-stu-id="cbff8-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="cbff8-114">Ardından JSON nesnesini `/api/books`' e gönderir.</span><span class="sxs-lookup"><span data-stu-id="cbff8-114">Then it POSTs the JSON object to `/api/books`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cbff8-115">[Önceki](part-8.md)
> [İleri](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="cbff8-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
