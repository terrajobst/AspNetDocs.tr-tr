---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: 'Bölüm 7: Ana sayfa oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599983"
---
# <a name="part-7-creating-the-main-page"></a><span data-ttu-id="5570e-102">Bölüm 7: Ana Sayfayı Oluşturma</span><span class="sxs-lookup"><span data-stu-id="5570e-102">Part 7: Creating the Main Page</span></span>

<span data-ttu-id="5570e-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5570e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="5570e-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="5570e-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a><span data-ttu-id="5570e-105">Ana Sayfayı Oluşturma</span><span class="sxs-lookup"><span data-stu-id="5570e-105">Creating the Main Page</span></span>

<span data-ttu-id="5570e-106">Bu bölümde, ana uygulama sayfası oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5570e-106">In this section, you will create the main application page.</span></span> <span data-ttu-id="5570e-107">Bu sayfa, yönetici sayfasından daha karmaşık olacaktır, bu nedenle bunu çeşitli adımlarda yaklaşıyoruz.</span><span class="sxs-lookup"><span data-stu-id="5570e-107">This page will be more complex than the Admin page, so we'll approach it in several steps.</span></span> <span data-ttu-id="5570e-108">Bu şekilde, daha gelişmiş altını gizleme. js tekniklerini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5570e-108">Along the way, you'll see some more advanced Knockout.js techniques.</span></span> <span data-ttu-id="5570e-109">Sayfanın temel düzeni aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5570e-109">Here is the basic layout of the page:</span></span>

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- <span data-ttu-id="5570e-110">"Ürünler" bir ürün dizisini tutar.</span><span class="sxs-lookup"><span data-stu-id="5570e-110">"Products" holds an array of products.</span></span>
- <span data-ttu-id="5570e-111">"Sepet" miktarları olan bir ürün dizisini tutar.</span><span class="sxs-lookup"><span data-stu-id="5570e-111">"Cart" holds an array of products with quantities.</span></span> <span data-ttu-id="5570e-112">"Sepete Ekle" seçeneğine tıkladığınızda sepette güncelleştirme yapılır.</span><span class="sxs-lookup"><span data-stu-id="5570e-112">Clicking "Add to Cart" updates the cart.</span></span>
- <span data-ttu-id="5570e-113">"Siparişler" bir sıra kimliği dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="5570e-113">"Orders" holds an array of order IDs.</span></span>
- <span data-ttu-id="5570e-114">"Ayrıntılar", bir dizi öğe olan (miktarları olan ürünler) bir sıra ayrıntısı tutar</span><span class="sxs-lookup"><span data-stu-id="5570e-114">"Details" holds an order detail, which is an array of items (products with quantities)</span></span>

<span data-ttu-id="5570e-115">HTML 'de veri bağlama veya betik olmadan bazı temel düzenleri tanımlayarak başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="5570e-115">We'll start by defining some basic layout in HTML, with no data binding or script.</span></span> <span data-ttu-id="5570e-116">Views/Home/Index. cshtml dosyasını açın ve tüm içeriği şu şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="5570e-116">Open the file Views/Home/Index.cshtml and replace all of the contents with the following:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

<span data-ttu-id="5570e-117">Sonra, bir komut dosyası bölümü ekleyin ve boş bir görünüm modeli oluşturun:</span><span class="sxs-lookup"><span data-stu-id="5570e-117">Next, add a Scripts section and create an empty view-model:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

<span data-ttu-id="5570e-118">Daha önce tasarım taslağı temel alınarak, görünüm modeliniz ürünler, sepet, siparişler ve Ayrıntılar için gözlemlenenler gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5570e-118">Based on the design sketched earlier, our view model needs observables for products, cart, orders, and details.</span></span> <span data-ttu-id="5570e-119">`AppViewModel` nesnesine aşağıdaki değişkenleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5570e-119">Add the following variables to the `AppViewModel` object:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

<span data-ttu-id="5570e-120">Kullanıcılar ürünler listesinden sepete öğeler ekleyebilir ve sepetten öğeleri kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="5570e-120">Users can add items from the products list into the cart, and remove items from the cart.</span></span> <span data-ttu-id="5570e-121">Bu işlevleri kapsüllemek için, bir ürünü temsil eden başka bir görünüm modeli sınıfı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="5570e-121">To encapsulate these functions, we'll create another view-model class that represents a product.</span></span> <span data-ttu-id="5570e-122">Aşağıdaki kodu `AppViewModel`ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5570e-122">Add the following code to `AppViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

<span data-ttu-id="5570e-123">`ProductViewModel` sınıfı, ürünü sepet içine ve sepetinden taşımak için kullanılan iki işlevi içerir: `addItemToCart` bir ürünün bir birimini sepete ekler ve `removeAllFromCart` ürünün tüm miktarlarını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="5570e-123">The `ProductViewModel` class contains two functions that are used to move the product to and from the cart: `addItemToCart` adds one unit of the product to the cart, and `removeAllFromCart` removes all quantities of the product.</span></span>

<span data-ttu-id="5570e-124">Kullanıcılar mevcut bir siparişi seçebilir ve sipariş ayrıntılarını alabilir.</span><span class="sxs-lookup"><span data-stu-id="5570e-124">Users can select an existing order and get the order details.</span></span> <span data-ttu-id="5570e-125">Bu işlevi başka bir görünüm modelinde kapsülliyoruz:</span><span class="sxs-lookup"><span data-stu-id="5570e-125">We'll encapsulate this functionality into another view-model:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

<span data-ttu-id="5570e-126">`OrderDetailsViewModel` bir siparişle başlatılır ve sunucuya bir AJAX isteği göndererek sipariş ayrıntılarını getirir.</span><span class="sxs-lookup"><span data-stu-id="5570e-126">The `OrderDetailsViewModel` is initialized with an order, and it fetches the order details by sending an AJAX request to the server.</span></span>

<span data-ttu-id="5570e-127">Ayrıca, `OrderDetailsViewModel``total` özelliğine de dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5570e-127">Also, notice the `total` property on the `OrderDetailsViewModel`.</span></span> <span data-ttu-id="5570e-128">Bu özellik, [hesaplanan observable](http://knockoutjs.com/documentation/computedObservables.html)adlı özel bir observable türüdür.</span><span class="sxs-lookup"><span data-stu-id="5570e-128">This property is a special kind of observable called a [computed observable](http://knockoutjs.com/documentation/computedObservables.html).</span></span> <span data-ttu-id="5570e-129">Adından da anlaşılacağı gibi, hesaplanan bir observable, bu durumda, siparişin toplam maliyeti olan&#8212;bir hesaplanan değere veri bağlamanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="5570e-129">As the name implies, a computed observable lets you data bind to a computed value&#8212;in this case, the total cost of the order.</span></span>

<span data-ttu-id="5570e-130">Sonra şu işlevleri `AppViewModel`ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5570e-130">Next, add these functions to `AppViewModel`:</span></span>

- <span data-ttu-id="5570e-131">`resetCart` tüm öğeleri sepetten kaldırır.</span><span class="sxs-lookup"><span data-stu-id="5570e-131">`resetCart` removes all items from the cart.</span></span>
- <span data-ttu-id="5570e-132">`getDetails` bir siparişin ayrıntılarını alır (`details` listesine yeni bir `OrderDetailsViewModel` göndererek).</span><span class="sxs-lookup"><span data-stu-id="5570e-132">`getDetails` gets the details for an order (by pushing a new `OrderDetailsViewModel` onto the `details` list).</span></span>
- <span data-ttu-id="5570e-133">`createOrder` yeni bir sipariş oluşturur ve sepeti boşaltır.</span><span class="sxs-lookup"><span data-stu-id="5570e-133">`createOrder` creates a new order and empties the cart.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

<span data-ttu-id="5570e-134">Son olarak, ürünler ve siparişler için AJAX istekleri yaparak görünüm modelini başlatın:</span><span class="sxs-lookup"><span data-stu-id="5570e-134">Finally, initialize the view model by making AJAX requests for the products and orders:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

<span data-ttu-id="5570e-135">Daha fazla kod olan Tamam, ancak adım adım bir adım geliştirdik, bu sayede tasarımın açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5570e-135">OK, that's a lot of code, but we built it up step-by-step, so hopefully the design is clear.</span></span> <span data-ttu-id="5570e-136">Artık HTML 'ye bazı altını gizleme. js bağlamaları ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="5570e-136">Now we can add some Knockout.js bindings to the HTML.</span></span>

<span data-ttu-id="5570e-137">**Ürünler**</span><span class="sxs-lookup"><span data-stu-id="5570e-137">**Products**</span></span>

<span data-ttu-id="5570e-138">Ürün listesinin bağlamaları aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5570e-138">Here are the bindings for the product list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

<span data-ttu-id="5570e-139">Bu, Products dizisinin üzerinde dolaşır ve adı ve fiyatı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5570e-139">This iterates over the products array and displays the name and price.</span></span> <span data-ttu-id="5570e-140">"Sıraya ekle" düğmesi yalnızca Kullanıcı oturum açtığında görünür.</span><span class="sxs-lookup"><span data-stu-id="5570e-140">The "Add to Order" button is visible only when the user is logged in.</span></span>

<span data-ttu-id="5570e-141">"Sıraya ekle" düğmesi, ürünün `ProductViewModel` örneğindeki `addItemToCart` çağırır.</span><span class="sxs-lookup"><span data-stu-id="5570e-141">The "Add to Order" button calls `addItemToCart` on the `ProductViewModel` instance for the product.</span></span> <span data-ttu-id="5570e-142">Bu, altını gizleme. js ' nin iyi bir özelliğini gösterir: Bir görünüm modeli diğer görünüm modellerini içerdiğinde, bağlamaları iç modele uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5570e-142">This demonstrates a nice feature of Knockout.js: When a view-model contains other view-models, you can apply the bindings to the inner model.</span></span> <span data-ttu-id="5570e-143">Bu örnekte, `foreach` içindeki bağlamalar `ProductViewModel` örneklerinin her birine uygulanır.</span><span class="sxs-lookup"><span data-stu-id="5570e-143">In this example, the bindings within the `foreach` are applied to each of the `ProductViewModel` instances.</span></span> <span data-ttu-id="5570e-144">Bu yaklaşım, tüm işlevleri tek bir görünüm modeline yerleştirmekten çok daha temizdir.</span><span class="sxs-lookup"><span data-stu-id="5570e-144">This approach is much cleaner than putting all of the functionality into a single view-model.</span></span>

<span data-ttu-id="5570e-145">**Cart**</span><span class="sxs-lookup"><span data-stu-id="5570e-145">**Cart**</span></span>

<span data-ttu-id="5570e-146">Sepetin bağlamaları aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5570e-146">Here are the bindings for the cart:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

<span data-ttu-id="5570e-147">Bu, sepet dizisinin üzerinde dolaşır ve adı, fiyatı ve miktarı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5570e-147">This iterates over the cart array and displays the name, price, and quantity.</span></span> <span data-ttu-id="5570e-148">"Kaldır" bağlantısının ve "sipariş oluştur" düğmesinin görünüm-model işlevlerine bağlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5570e-148">Note that the "Remove" link and the "Create Order" button are bound to view-model functions.</span></span>

<span data-ttu-id="5570e-149">**Siparişlerine**</span><span class="sxs-lookup"><span data-stu-id="5570e-149">**Orders**</span></span>

<span data-ttu-id="5570e-150">Siparişler listesinin bağlamaları aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5570e-150">Here are the bindings for the orders list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

<span data-ttu-id="5570e-151">Bu, siparişlerin üzerinde dolaşır ve sipariş KIMLIĞINI gösterir.</span><span class="sxs-lookup"><span data-stu-id="5570e-151">This iterates over the orders and shows the order ID.</span></span> <span data-ttu-id="5570e-152">Bağlantıdaki tıklama olayı `getDetails` işlevine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5570e-152">The click event on the link is bound to the `getDetails` function.</span></span>

<span data-ttu-id="5570e-153">**Sipariş Ayrıntıları**</span><span class="sxs-lookup"><span data-stu-id="5570e-153">**Order Details**</span></span>

<span data-ttu-id="5570e-154">Sıra ayrıntılarının bağlamaları aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5570e-154">Here are the bindings for the order details:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

<span data-ttu-id="5570e-155">Bu, siparişteki öğeleri yineler ve ürünü, fiyatı ve miktarı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5570e-155">This iterates over the items in the order and displays the product, price, and quantity.</span></span> <span data-ttu-id="5570e-156">Çevreleyen div yalnızca details dizisi bir veya daha fazla öğe içeriyorsa görünür.</span><span class="sxs-lookup"><span data-stu-id="5570e-156">The surrounding div is visible only if the details array contains one or more items.</span></span>

## <a name="conclusion"></a><span data-ttu-id="5570e-157">Sonuç</span><span class="sxs-lookup"><span data-stu-id="5570e-157">Conclusion</span></span>

<span data-ttu-id="5570e-158">Bu öğreticide, veritabanıyla iletişim kurmak için Entity Framework kullanan bir uygulama oluşturdunuz ve veri katmanının en üstünde herkese açık bir arabirim sağlamak için ASP.NET Web API 'SI.</span><span class="sxs-lookup"><span data-stu-id="5570e-158">In this tutorial, you created an application that uses Entity Framework to communicate with the database, and ASP.NET Web API to provide a public-facing interface on top of the data layer.</span></span> <span data-ttu-id="5570e-159">HTML sayfalarını işlemek için ASP.NET MVC 4, sayfa yeniden yüklemeye gerek kalmadan dinamik etkileşimler sağlamak için de altını gizleme. js ' yi kullanırız.</span><span class="sxs-lookup"><span data-stu-id="5570e-159">We use ASP.NET MVC 4 to render the HTML pages, and Knockout.js plus jQuery to provide dynamic interactions without page reloads.</span></span>

<span data-ttu-id="5570e-160">Ek kaynaklar:</span><span class="sxs-lookup"><span data-stu-id="5570e-160">Additional resources:</span></span>

- [<span data-ttu-id="5570e-161">ASP.NET veri erişimi Içerik Haritası</span><span class="sxs-lookup"><span data-stu-id="5570e-161">ASP.NET Data Access Content Map</span></span>](https://msdn.microsoft.com/library/6759sth4.aspx)
- [<span data-ttu-id="5570e-162">Entity Framework Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="5570e-162">Entity Framework Developer Center</span></span>](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [<span data-ttu-id="5570e-163">Önceki</span><span class="sxs-lookup"><span data-stu-id="5570e-163">Previous</span></span>](using-web-api-with-entity-framework-part-6.md)
