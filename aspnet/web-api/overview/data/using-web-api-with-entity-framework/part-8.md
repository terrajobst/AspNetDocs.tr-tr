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
# <a name="display-item-details"></a><span data-ttu-id="ffff1-102">Öğe Ayrıntılarını Görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ffff1-102">Display Item Details</span></span>

<span data-ttu-id="ffff1-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ffff1-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ffff1-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="ffff1-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="ffff1-105">Bu bölümde, her bir kitabın ayrıntılarını görüntüleme özelliğini ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="ffff1-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="ffff1-106">App. js ' de, görünüm modeline aşağıdaki koda ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ffff1-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="ffff1-107">Görünümler/Home/Index. cshtml 'de, Ayrıntılar bağlantısına bir veri bağlama öğesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ffff1-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="ffff1-108">Bu, bir&gt; öğesi &lt;için tıklama işleyicisini görünüm modelindeki `getBookDetail` işlevine bağlar.</span><span class="sxs-lookup"><span data-stu-id="ffff1-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="ffff1-109">Aynı dosyada, aşağıdaki işareti değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ffff1-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="ffff1-110">şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ffff1-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="ffff1-111">Bu biçimlendirme, görünüm modelinde `detail` observable özelliklerine veri bağlanan bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ffff1-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="ffff1-112">"&lt;!--Ko--&gt;&quot; sözdizimi, DOM öğesinin dışında bir altını gizleme bağlamayı eklemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ffff1-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="ffff1-113">Bu durumda `if` bağlama, biçimlendirmenin bu bölümünün yalnızca `details` null olmadığı durumlarda görüntülenmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="ffff1-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="ffff1-114">Uygulamayı çalıştırıp &quot;ayrıntılarından birine&quot; bağlantılardan birine tıklarsanız, uygulama kitap ayrıntılarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ffff1-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="ffff1-115">[Önceki](part-7.md)
> [İleri](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="ffff1-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>
