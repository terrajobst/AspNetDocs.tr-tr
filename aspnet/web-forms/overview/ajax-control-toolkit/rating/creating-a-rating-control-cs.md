---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: Derecelendirme denetimi oluşturma (C#) | Microsoft Docs
author: wenz
description: E-ticaretin topluluk sitelerine kadar birçok Web sitesi, kullanıcılarını makale veya öğe hızına sunmaya olanak sağlar. Bu genellikle bazı kodlama çabaları gerektirir, ancak...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: c0bf793406e378321f54f0460031c526a0b41a02
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611559"
---
# <a name="creating-a-rating-control-c"></a><span data-ttu-id="44807-104">Derecelendirme Denetimi Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="44807-104">Creating a Rating Control (C#)</span></span>

<span data-ttu-id="44807-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="44807-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="44807-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="44807-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="44807-107">E-ticaretin topluluk sitelerine kadar birçok Web sitesi, kullanıcılarını makale veya öğe hızına sunmaya olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="44807-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="44807-108">Bu genellikle bazı kodlama çabaları gerektirir, ancak elden çıkarılmız için Denetim araç seti vardır.</span><span class="sxs-lookup"><span data-stu-id="44807-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="overview"></a><span data-ttu-id="44807-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="44807-109">Overview</span></span>

<span data-ttu-id="44807-110">E-ticaretin topluluk sitelerine kadar birçok Web sitesi, kullanıcılarını makale veya öğe hızına sunmaya olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="44807-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="44807-111">Bu genellikle bazı kodlama çabaları gerektirir, ancak elden çıkarılmız için Denetim araç seti vardır.</span><span class="sxs-lookup"><span data-stu-id="44807-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="44807-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="44807-112">Steps</span></span>

<span data-ttu-id="44807-113">Birincisi, bir tanesi doldurulmuş bir derecelendirme öğesi ve diğeri de boş bir derecelendirme öğesi için (en az) iki tür görüntü gerekir.</span><span class="sxs-lookup"><span data-stu-id="44807-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="44807-114">Bir derecelendirme öğesi genellikle bir yıldız veya gülümseme olur.</span><span class="sxs-lookup"><span data-stu-id="44807-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="44807-115">Bu senaryo için, bu öğreticide kaynak kodu indirmelerinin bir parçası olarak gülümseme. png ve Empty. png ve Smiley-done. png olmak üzere üç dosya bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44807-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="44807-116">Ardından, yeni bir ASP.NET dosyası oluşturun ve buna `ScriptManager` denetimi ekleyerek başlayın:</span><span class="sxs-lookup"><span data-stu-id="44807-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="44807-117">Sonra, ASP.NET AJAX denetim araç seti ' nden `Rating` denetimini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="44807-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="44807-118">Bu örnek için aşağıdaki özniteliklerin ayarlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="44807-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="44807-119">kullanılacak ilk derecelendirmeyi `CurrentRating`</span><span class="sxs-lookup"><span data-stu-id="44807-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="44807-120">maksimum derecelendirmeyi `MaxRating`</span><span class="sxs-lookup"><span data-stu-id="44807-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="44807-121">bir derecelendirme öğesi (yıldız) boş olduğunda kullanılacak CSS sınıfını `EmptyStarCssClass`</span><span class="sxs-lookup"><span data-stu-id="44807-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="44807-122">bir derecelendirme öğesi (yıldız) dolduğunda kullanılacak CSS sınıfını `FilledStarCssClass`</span><span class="sxs-lookup"><span data-stu-id="44807-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="44807-123">görünür bir stat için kullanılacak CSS sınıfını `StarCssClass`</span><span class="sxs-lookup"><span data-stu-id="44807-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="44807-124">bir yıldız derecelendirmesi sunucuya geri gönderildiğinde kullanılacak CSS sınıfını `WaitingStarCssClass`</span><span class="sxs-lookup"><span data-stu-id="44807-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="44807-125">Burada, başlangıçta hiçbirinin doldurulduğu beş öğe (Smileys) ile bir derecelendirme denetimi oluşturan biçimlendirme verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="44807-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="44807-126">Şu anda başvurulan üç CSS sınıfı, CSS kullanılarak kolayca yapılacak uygun görüntü dosyalarını göstermeye gerek duyar:</span><span class="sxs-lookup"><span data-stu-id="44807-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="44807-127">Üç görüntünün genişlik ve yüksekliğini sağladığınızdan emin olun, aksi takdirde ekran bir bit ileti olarak görünebilir.</span><span class="sxs-lookup"><span data-stu-id="44807-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="44807-128">Son olarak, derecelendirmenin sonucu kullanıcıya (veya en azından bir veritabanında kayıtlı) gösterilmelidir.</span><span class="sxs-lookup"><span data-stu-id="44807-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="44807-129">Bu nedenle, derecelendirme formunu sunucuya göndermek için bir kısa mesaj ve Gönder düğmesinin çıktısı için bir etiket ekleyin:</span><span class="sxs-lookup"><span data-stu-id="44807-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="44807-130">Sunucu tarafı kodunda, derecelendirme denetimine `ID` aracılığıyla erişin ve sonra, örnek 0 ile 5 arasında bir değer olan seçili derecelendirme öğelerinin sayısı olan `CurrentRating` özelliğine erişin.</span><span class="sxs-lookup"><span data-stu-id="44807-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="44807-131">Sayfayı kaydedin ve tarayıcınıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="44807-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="44807-132">(Başlangıçta boş) derecelendirme öğelerinin üzerine geldiğinizde bir JavaScript etkisi oluşur: derecelendirme değişir.</span><span class="sxs-lookup"><span data-stu-id="44807-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="44807-133">Yıldız kümesine tıkladığınızda, geçerli derecelendirme korunur.</span><span class="sxs-lookup"><span data-stu-id="44807-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="44807-134">Son olarak, formu gönderdiğinizde, sunucu tarafı kodu seçili derecelendirmeyi çıktı.</span><span class="sxs-lookup"><span data-stu-id="44807-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>

<span data-ttu-id="44807-135">[en az kodla bir derecelendirme sistemi oluşturma ![](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="44807-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="44807-136">Minimum kodla bir derecelendirme sistemi oluşturma ([tam boyutlu görüntüyü görüntülemek Için tıklayın](creating-a-rating-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="44807-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="44807-137">Next</span><span class="sxs-lookup"><span data-stu-id="44807-137">Next</span></span>](creating-a-rating-control-vb.md)
