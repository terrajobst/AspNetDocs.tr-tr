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
# <a name="create-the-view-ui"></a><span data-ttu-id="d99b1-102">Görünümü (Kullanıcı Arabirimi) Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d99b1-102">Create the View (UI)</span></span>

<span data-ttu-id="d99b1-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d99b1-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="d99b1-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="d99b1-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="d99b1-105">Bu bölümde, uygulamanın HTML 'sini tanımlamaya ve HTML ile görünüm modeli arasında veri bağlama eklemeye başlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d99b1-105">In this section, you will start to define the HTML for the app, and add data binding between the HTML and the view model.</span></span>

<span data-ttu-id="d99b1-106">Views/Home/Index. cshtml dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d99b1-106">Open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="d99b1-107">Bu dosyanın tüm içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d99b1-107">Replace the entire contents of that file with the following.</span></span>

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

<span data-ttu-id="d99b1-108">`div` öğelerinin çoğu [önyükleme](http://getbootstrap.com/) stili için vardır.</span><span class="sxs-lookup"><span data-stu-id="d99b1-108">Most of the `div` elements are there for [Bootstrap](http://getbootstrap.com/) styling.</span></span> <span data-ttu-id="d99b1-109">Önemli öğeler `data-bind` öznitelikleridir.</span><span class="sxs-lookup"><span data-stu-id="d99b1-109">The important elements are the ones with `data-bind` attributes.</span></span> <span data-ttu-id="d99b1-110">Bu öznitelik HTML 'i görünüm modeline bağlar.</span><span class="sxs-lookup"><span data-stu-id="d99b1-110">This attribute links the HTML to the view model.</span></span>

<span data-ttu-id="d99b1-111">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d99b1-111">For example:</span></span>

[!code-html[Main](part-7/samples/sample2.html)]

<span data-ttu-id="d99b1-112">Bu örnekte, &quot;`text`&quot; bağlama `<p>` öğenin görünüm modelinden `error` özelliğinin değerini göstermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d99b1-112">In this example, the &quot;`text`&quot; binding causes the `<p>` element to show the value of the `error` property from the view model.</span></span> <span data-ttu-id="d99b1-113">`error` `ko.observable`olarak bildirildiği hatırlayın:</span><span class="sxs-lookup"><span data-stu-id="d99b1-113">Recall that `error` was declared as a `ko.observable`:</span></span>

[!code-javascript[Main](part-7/samples/sample3.js)]

<span data-ttu-id="d99b1-114">`error`için yeni bir değer atandığında, altını Gizle `<p>` öğesindeki metni günceller.</span><span class="sxs-lookup"><span data-stu-id="d99b1-114">Whenever a new value is assigned to `error`, Knockout updates the text in the `<p>` element.</span></span>

<span data-ttu-id="d99b1-115">`foreach` bağlama, altını gizlemeyi `books` dizisinin içerikleri aracılığıyla döngüye bildirir.</span><span class="sxs-lookup"><span data-stu-id="d99b1-115">The `foreach` binding tells Knockout to loop through the contents of the `books` array.</span></span> <span data-ttu-id="d99b1-116">Dizideki her öğe için, altını gizleme yeni bir &lt;li&gt; öğesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d99b1-116">For each item in the array, Knockout creates a new &lt;li&gt; element.</span></span> <span data-ttu-id="d99b1-117">`foreach` bağlamı içindeki bağlamalar, dizi öğesindeki özelliklere başvurur.</span><span class="sxs-lookup"><span data-stu-id="d99b1-117">Bindings inside the context of the `foreach` refer to properties on the array item.</span></span> <span data-ttu-id="d99b1-118">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d99b1-118">For example:</span></span>

[!code-html[Main](part-7/samples/sample4.html)]

<span data-ttu-id="d99b1-119">Burada `text` bağlama her kitabın Author özelliğini okur.</span><span class="sxs-lookup"><span data-stu-id="d99b1-119">Here the `text` binding reads the Author property of each book.</span></span>

<span data-ttu-id="d99b1-120">Uygulamayı şimdi çalıştırırsanız, şöyle görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="d99b1-120">If you run the application now, it should look like this:</span></span>

![](part-7/_static/image1.png)

<span data-ttu-id="d99b1-121">Kitaplar Listesi, sayfa yüklendikten sonra zaman uyumsuz olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d99b1-121">The list of books loads asynchronously, after the page loads.</span></span> <span data-ttu-id="d99b1-122">Şu anda &quot;ayrıntıları&quot; bağlantılar işlevsel değildir.</span><span class="sxs-lookup"><span data-stu-id="d99b1-122">Right now, the &quot;Details&quot; links are not functional.</span></span> <span data-ttu-id="d99b1-123">Sonraki bölümde bu işlevselliği ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d99b1-123">We'll add this functionality in the next section.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d99b1-124">[Önceki](part-6.md)
> [İleri](part-8.md)</span><span class="sxs-lookup"><span data-stu-id="d99b1-124">[Previous](part-6.md)
[Next](part-8.md)</span></span>
