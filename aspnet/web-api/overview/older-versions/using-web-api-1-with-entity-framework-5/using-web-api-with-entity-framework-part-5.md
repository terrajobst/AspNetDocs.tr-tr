---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: '5\. Bölüm: altını gizleme. js ile dinamik kullanıcı arabirimi oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555995"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="49e9c-102">5\. Bölüm: altını gizleme. js ile dinamik kullanıcı arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="49e9c-102">Part 5: Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="49e9c-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="49e9c-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="49e9c-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="49e9c-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="49e9c-105">Knockout.js ile Dinamik Kullanıcı Arabirimi Oluşturma</span><span class="sxs-lookup"><span data-stu-id="49e9c-105">Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="49e9c-106">Bu bölümde, yönetici görünümüne işlevsellik eklemek için altını gizleme. js ' yi kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="49e9c-106">In this section, we'll use Knockout.js to add functionality to the Admin view.</span></span>

<span data-ttu-id="49e9c-107">[Altını gizleme. js](http://knockoutjs.com/) , HTML denetimlerini verilere bağlamayı kolaylaştıran bir JavaScript kitaplığıdır.</span><span class="sxs-lookup"><span data-stu-id="49e9c-107">[Knockout.js](http://knockoutjs.com/) is a Javascript library that makes it easy to bind HTML controls to data.</span></span> <span data-ttu-id="49e9c-108">Altını gizleme. js Model-View-ViewModel (MVVM) modelini kullanır.</span><span class="sxs-lookup"><span data-stu-id="49e9c-108">Knockout.js uses the Model-View-ViewModel (MVVM) pattern.</span></span>

- <span data-ttu-id="49e9c-109">*Model* , iş etki alanındaki verilerin sunucu tarafı gösterimidir (bizim örneğimizde, ürünlerimiz ve siparişlerde).</span><span class="sxs-lookup"><span data-stu-id="49e9c-109">The *model* is the server-side representation of the data in the business domain (in our case, products and orders).</span></span>
- <span data-ttu-id="49e9c-110">*Görünüm* sunum katmanıdır (HTML).</span><span class="sxs-lookup"><span data-stu-id="49e9c-110">The *view* is the presentation layer (HTML).</span></span>
- <span data-ttu-id="49e9c-111">*View-model* , model verilerini tutan bir JavaScript nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="49e9c-111">The *view-model* is a Javascript object that holds the model data.</span></span> <span data-ttu-id="49e9c-112">View-model, Kullanıcı arabiriminin kod soyutlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="49e9c-112">The view-model is a code abstraction of the UI.</span></span> <span data-ttu-id="49e9c-113">HTML temsili bilgisine sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="49e9c-113">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="49e9c-114">Bunun yerine, görünümün "öğe listesi" gibi soyut özelliklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="49e9c-114">Instead, it represents abstract features of the view, such as "a list of items".</span></span>

<span data-ttu-id="49e9c-115">Görünüm, görünüm modeline veri ile bağlanır.</span><span class="sxs-lookup"><span data-stu-id="49e9c-115">The view is data-bound to the view-model.</span></span> <span data-ttu-id="49e9c-116">Görünüm modeli güncelleştirmeleri otomatik olarak görünüme yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="49e9c-116">Updates to the view-model are automatically reflected in the view.</span></span> <span data-ttu-id="49e9c-117">Görünüm modeli Ayrıca, düğme tıklamaları gibi görünümden olayları alır ve model üzerinde bir sipariş oluşturma gibi işlemleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="49e9c-117">The view-model also gets events from the view, such as button clicks, and performs operations on the model, such as creating an order.</span></span>

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

<span data-ttu-id="49e9c-118">İlk olarak View-model tanımlayacağız.</span><span class="sxs-lookup"><span data-stu-id="49e9c-118">First we'll define the view-model.</span></span> <span data-ttu-id="49e9c-119">Bundan sonra, HTML işaretlemesini görünüm modeline bağlayacağız.</span><span class="sxs-lookup"><span data-stu-id="49e9c-119">After that, we will bind the HTML markup to the view-model.</span></span>

<span data-ttu-id="49e9c-120">Aşağıdaki Razor bölümünü admin. cshtml öğesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="49e9c-120">Add the following Razor section to Admin.cshtml:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

<span data-ttu-id="49e9c-121">Bu bölümü dosyada herhangi bir yere ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49e9c-121">You can add this section anywhere in the file.</span></span> <span data-ttu-id="49e9c-122">Görünüm işlendiğinde, Bölüm HTML sayfasının alt kısmında, kapatma &lt;/Body&gt; etiketinden hemen önce görünür.</span><span class="sxs-lookup"><span data-stu-id="49e9c-122">When the view is rendered, the section appears at the bottom of the HTML page, right before the closing &lt;/body&gt; tag.</span></span>

<span data-ttu-id="49e9c-123">Bu sayfanın tüm betiği, yorum tarafından belirtilen komut dosyası etiketinin içine alınacaktır:</span><span class="sxs-lookup"><span data-stu-id="49e9c-123">All of the script for this page will go inside the script tag indicated by the comment:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

<span data-ttu-id="49e9c-124">İlk olarak, bir View-model sınıfı tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="49e9c-124">First, define a view-model class:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

<span data-ttu-id="49e9c-125">**ko. observableArray** , bir *observable*olarak adlandırılan, altını gizleme içindeki özel bir nesne türüdür.</span><span class="sxs-lookup"><span data-stu-id="49e9c-125">**ko.observableArray** is a special kind of object in Knockout, called an *observable*.</span></span> <span data-ttu-id="49e9c-126">[Altını gizleme. js belgelerinden](http://knockoutjs.com/documentation/observables.html): bir observable, abonelere değişiklikler hakkında bildirimde bulunan bir "JavaScript nesnesidir."</span><span class="sxs-lookup"><span data-stu-id="49e9c-126">From the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html): An observable is a "JavaScript object that can notify subscribers about changes."</span></span> <span data-ttu-id="49e9c-127">Bir observable 'ın içeriği değiştiğinde görünüm, eşleşecek şekilde otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="49e9c-127">When the contents of an observable change, the view is automatically updated to match.</span></span>

<span data-ttu-id="49e9c-128">`products` diziyi doldurmak için Web API 'sine bir AJAX isteği yapın.</span><span class="sxs-lookup"><span data-stu-id="49e9c-128">To populate the `products` array, make an AJAX request to the web API.</span></span> <span data-ttu-id="49e9c-129">Görünüm paketinde API için temel URI 'yi depoladığımızda hatırlayın (öğreticinin 4. [bölümüne](using-web-api-with-entity-framework-part-4.md) bakın).</span><span class="sxs-lookup"><span data-stu-id="49e9c-129">Recall that we stored the base URI for the API in the view bag (see [Part 4](using-web-api-with-entity-framework-part-4.md) of the tutorial).</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

<span data-ttu-id="49e9c-130">Ardından, Products oluşturmak, güncelleştirmek ve silmek için View-model ' e işlevler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="49e9c-130">Next, add functions to the view-model to create, update, and delete products.</span></span> <span data-ttu-id="49e9c-131">Bu işlevler, Web API 'sine AJAX çağrıları gönderir ve sonuçları kullanarak görünüm modelini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="49e9c-131">These functions submit AJAX calls to the web API and use the results to update the view-model.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

<span data-ttu-id="49e9c-132">Şimdi en önemli bölüm: DOM daha fazla yüklendiğinde, **ko. applyBindings** işlevini çağırın ve `ProductsViewModel`yeni bir örneğini geçirin:</span><span class="sxs-lookup"><span data-stu-id="49e9c-132">Now the most important part: When the DOM is fulled loaded, call the **ko.applyBindings** function and pass in a new instance of the `ProductsViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

<span data-ttu-id="49e9c-133">**Ko. applyBindings** yöntemi, gizlemeyi etkinleştirir ve görünüm modelini görünüme bağlar.</span><span class="sxs-lookup"><span data-stu-id="49e9c-133">The **ko.applyBindings** method activates Knockout and wires up the view-model to the view.</span></span>

<span data-ttu-id="49e9c-134">Artık bir görünüm modelimiz olduğuna göre, bağlamaları oluşturarız.</span><span class="sxs-lookup"><span data-stu-id="49e9c-134">Now that we have a view-model, we can create the bindings.</span></span> <span data-ttu-id="49e9c-135">Altını gizleme. js ' de, bunu HTML öğelerine `data-bind` öznitelikleri ekleyerek yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49e9c-135">In Knockout.js, you do this by adding `data-bind` attributes to HTML elements.</span></span> <span data-ttu-id="49e9c-136">Örneğin, bir HTML listesini diziye bağlamak için `foreach` bağlamayı kullanın:</span><span class="sxs-lookup"><span data-stu-id="49e9c-136">For example, to bind an HTML list to an array, use the `foreach` binding:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

<span data-ttu-id="49e9c-137">`foreach` bağlama, dizi boyunca yinelenir ve dizideki her nesne için alt öğeler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="49e9c-137">The `foreach` binding iterates through the array and creates child elements for each object in the array.</span></span> <span data-ttu-id="49e9c-138">Alt öğelerdeki bağlamalar, dizi nesnelerinde özelliklere başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="49e9c-138">Bindings on the child elements can refer to properties on the array objects.</span></span>

<span data-ttu-id="49e9c-139">Aşağıdaki bağlamaları "Update-Products" listesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="49e9c-139">Add the following bindings to the "update-products" list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

<span data-ttu-id="49e9c-140">`<li>` öğesi, **foreach** bağlamasının kapsamı içinde meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="49e9c-140">The `<li>` element occurs within the scope of the **foreach** binding.</span></span> <span data-ttu-id="49e9c-141">Bunun anlamı, `products` dizisindeki her ürün için öğeyi bir kez oluşturacak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="49e9c-141">That means Knockout will render the element once for each product in the `products` array.</span></span> <span data-ttu-id="49e9c-142">`<li>` öğesi içindeki tüm bağlamalar, bu ürün örneğine başvurur.</span><span class="sxs-lookup"><span data-stu-id="49e9c-142">All of the bindings within the `<li>` element refer to that product instance.</span></span> <span data-ttu-id="49e9c-143">Örneğin, `$data.Name` üründeki `Name` özelliğine başvurur.</span><span class="sxs-lookup"><span data-stu-id="49e9c-143">For example, `$data.Name` refers to the `Name` property on the product.</span></span>

<span data-ttu-id="49e9c-144">Metin girişlerinin değerlerini ayarlamak için `value` bağlamayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="49e9c-144">To set the values of the text inputs, use the `value` binding.</span></span> <span data-ttu-id="49e9c-145">Düğmeler, `click` bağlamasını kullanarak model görünümündeki işlevlere bağlanır.</span><span class="sxs-lookup"><span data-stu-id="49e9c-145">The buttons are bound to functions on the model-view, using the `click` binding.</span></span> <span data-ttu-id="49e9c-146">Ürün örneği her işleve bir parametre olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="49e9c-146">The product instance is passed as a parameter to each function.</span></span> <span data-ttu-id="49e9c-147">Daha fazla bilgi için, [altını gizleme. js belgeleri](http://knockoutjs.com/documentation/observables.html) çeşitli bağlamaların iyi açıklamalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="49e9c-147">For more information, the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html) has good descriptions of the various bindings.</span></span>

<span data-ttu-id="49e9c-148">Ardından, ürün Ekle formundaki **Gönder** olayı için bir bağlama ekleyin:</span><span class="sxs-lookup"><span data-stu-id="49e9c-148">Next, add a binding for the **submit** event on the Add Product form:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

<span data-ttu-id="49e9c-149">Bu bağlama, yeni bir ürün oluşturmak için görünüm modelinde `create` işlevini çağırır.</span><span class="sxs-lookup"><span data-stu-id="49e9c-149">This binding calls the `create` function on the view-model to create a new product.</span></span>

<span data-ttu-id="49e9c-150">Yönetici görünümü için kodun tamamı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="49e9c-150">Here is the complete code for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

<span data-ttu-id="49e9c-151">Uygulamayı çalıştırın, yönetici hesabıyla oturum açın ve "Yönetici" bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="49e9c-151">Run the application, log in with the Administrator account, and click the "Admin" link.</span></span> <span data-ttu-id="49e9c-152">Ürünlerin listesini görmeniz ve ürün oluşturabilir, güncelleştirebilir veya silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49e9c-152">You should see the list of products, and be able to create, update, or delete products.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="49e9c-153">[Önceki](using-web-api-with-entity-framework-part-4.md)
> [İleri](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="49e9c-153">[Previous](using-web-api-with-entity-framework-part-4.md)
[Next](using-web-api-with-entity-framework-part-6.md)</span></span>
