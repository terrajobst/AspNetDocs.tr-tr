---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: Veri öğelerini ve ayrıntıları görüntüleme | Microsoft Docs
author: Erikre
description: Bu öğretici serisinde, ASP.NET 4,7 ve Microsoft Visual Studio 2017 ile bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgiler gösterilir
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641115"
---
# <a name="display-data-items-and-details"></a><span data-ttu-id="b6093-103">Veri öğelerini ve ayrıntılarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b6093-103">Display data items and details</span></span>

<span data-ttu-id="b6093-104">by [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="b6093-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="b6093-105">Bu öğretici serisi, ASP.NET 4,7 ve Microsoft Visual Studio 2017 ile bir ASP.NET Web Forms uygulamasının oluşturulmasına ilişkin temel bilgileri öğretir.</span><span class="sxs-lookup"><span data-stu-id="b6093-105">This tutorial series teaches you the basics of building an ASP.NET Web Forms application with ASP.NET 4.7 and Microsoft Visual Studio 2017.</span></span>

<span data-ttu-id="b6093-106">Bu öğreticide, ASP.NET Web Forms ve Code First Entity Framework ile veri öğelerini ve veri öğesi ayrıntılarını görüntülemeyi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b6093-106">In this tutorial, you'll learn how to display data items and data item details with ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="b6093-107">Bu öğretici, Wingtip Oyunstore öğretici serisinin bir parçası olarak önceki "UI ve gezinti" öğreticisini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b6093-107">This tutorial builds on the previous "UI and Navigation" tutorial as part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="b6093-108">Bu Öğreticiyi tamamladıktan sonra *Productslist. aspx* sayfasında ürünleri ve *ProductDetails. aspx* sayfasında bir ürünün ayrıntılarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b6093-108">After completing this tutorial, you'll see products on the *ProductsList.aspx* page and a product's details on the *ProductDetails.aspx* page.</span></span>

## <a name="youll-learn-how-to"></a><span data-ttu-id="b6093-109">Şunları öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b6093-109">You'll learn how to:</span></span>

- <span data-ttu-id="b6093-110">Veritabanındaki ürünleri göstermek için bir veri denetimi ekleyin</span><span class="sxs-lookup"><span data-stu-id="b6093-110">Add a data control to display products from the database</span></span>
- <span data-ttu-id="b6093-111">Veri denetimini seçili verilere bağlama</span><span class="sxs-lookup"><span data-stu-id="b6093-111">Connect a data control to the selected data</span></span>
- <span data-ttu-id="b6093-112">Veritabanından ürün ayrıntılarını göstermek için bir veri denetimi ekleyin</span><span class="sxs-lookup"><span data-stu-id="b6093-112">Add a data control to display product details from the database</span></span>
- <span data-ttu-id="b6093-113">Sorgu dizesinden bir değer alın ve veritabanından alınan verileri sınırlamak için bu değeri kullanın</span><span class="sxs-lookup"><span data-stu-id="b6093-113">Retrieve a value from the query string and use that value to limit the data that's retrieved from the database</span></span>

### <a name="features-introduced-in-this-tutorial"></a><span data-ttu-id="b6093-114">Bu öğreticide tanıtılan Özellikler:</span><span class="sxs-lookup"><span data-stu-id="b6093-114">Features introduced in this tutorial:</span></span>

- <span data-ttu-id="b6093-115">Model bağlama</span><span class="sxs-lookup"><span data-stu-id="b6093-115">Model binding</span></span>
- <span data-ttu-id="b6093-116">Değer sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="b6093-116">Value providers</span></span>

## <a name="add-a-data-control"></a><span data-ttu-id="b6093-117">Veri denetimi ekleme</span><span class="sxs-lookup"><span data-stu-id="b6093-117">Add a data control</span></span>

<span data-ttu-id="b6093-118">Bir sunucu denetimine veri bağlamak için birkaç farklı seçenek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6093-118">You can use a few different options to bind data to a server control.</span></span> <span data-ttu-id="b6093-119">En yaygın şunlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b6093-119">The most common include:</span></span>

* <span data-ttu-id="b6093-120">Veri kaynağı denetimi ekleme</span><span class="sxs-lookup"><span data-stu-id="b6093-120">Adding a data source control</span></span>
* <span data-ttu-id="b6093-121">El ile kod ekleme</span><span class="sxs-lookup"><span data-stu-id="b6093-121">Adding code by hand</span></span>
* <span data-ttu-id="b6093-122">Model bağlamayı kullanma</span><span class="sxs-lookup"><span data-stu-id="b6093-122">Using model binding</span></span>

### <a name="use-a-data-source-control-to-bind-data"></a><span data-ttu-id="b6093-123">Veri bağlamak için bir veri kaynağı denetimi kullanın</span><span class="sxs-lookup"><span data-stu-id="b6093-123">Use a data source control to bind data</span></span>

<span data-ttu-id="b6093-124">Veri kaynağı denetimi eklemek, veri kaynağı denetimini verileri görüntüleyen denetime bağlayabilmeniz için izin verir.</span><span class="sxs-lookup"><span data-stu-id="b6093-124">Adding a data source control allows you to link the data source control to the control that displays the data.</span></span> <span data-ttu-id="b6093-125">Bu yaklaşımda, programlı olarak değil, sunucu tarafı denetimlerini veri kaynaklarına bağlamak için bildirimli olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6093-125">With this approach, you can declaratively,  rather than programmatically, connect server-side controls to data sources.</span></span>

### <a name="code-by-hand-to-bind-data"></a><span data-ttu-id="b6093-126">Verileri bağlamak için el ile kod</span><span class="sxs-lookup"><span data-stu-id="b6093-126">Code by hand to bind data</span></span>

<span data-ttu-id="b6093-127">El ile kodlama şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="b6093-127">Coding by hand involves:</span></span>

1. <span data-ttu-id="b6093-128">Bir değer okunuyor</span><span class="sxs-lookup"><span data-stu-id="b6093-128">Reading a value</span></span>
2. <span data-ttu-id="b6093-129">Null olup olmadığı denetleniyor</span><span class="sxs-lookup"><span data-stu-id="b6093-129">Checking if it's null</span></span>
3. <span data-ttu-id="b6093-130">Uygun bir türe dönüştürülüyor</span><span class="sxs-lookup"><span data-stu-id="b6093-130">Converting it to an appropriate type</span></span>
4. <span data-ttu-id="b6093-131">Dönüştürme başarılı denetleniyor</span><span class="sxs-lookup"><span data-stu-id="b6093-131">Checking conversion success</span></span>
5. <span data-ttu-id="b6093-132">Sorgudaki değeri kullanma</span><span class="sxs-lookup"><span data-stu-id="b6093-132">Using the value in the query</span></span> 

<span data-ttu-id="b6093-133">Bu yaklaşım, veri erişim mantığınız üzerinde tam denetime sahip olmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6093-133">This approach lets you have full control over your data-access logic.</span></span>

### <a name="use-model-binding-to-bind-data"></a><span data-ttu-id="b6093-134">Veri bağlamak için model bağlamayı kullanma</span><span class="sxs-lookup"><span data-stu-id="b6093-134">Use model binding to bind data</span></span>

<span data-ttu-id="b6093-135">Model bağlama, sonuçları çok daha az kodla bağlamanızı sağlar ve uygulamanızı genelinde işlevselliği yeniden kullanma olanağı sunar.</span><span class="sxs-lookup"><span data-stu-id="b6093-135">Model binding lets you bind results with far less code and gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="b6093-136">Hala zengin, veri bağlama çerçevesi sağlarken kod odaklı veri erişim mantığı ile çalışmayı basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="b6093-136">It simplifies working with code-focused data-access logic while still providing a rich, data-binding framework.</span></span>

## <a name="display-products"></a><span data-ttu-id="b6093-137">Ürünleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b6093-137">Display products</span></span>

<span data-ttu-id="b6093-138">Bu öğreticide, veri bağlamak için model bağlamayı kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b6093-138">In this tutorial, you'll use model binding to bind data.</span></span> <span data-ttu-id="b6093-139">Veri seçmek üzere model bağlamayı kullanmak üzere bir veri denetimi yapılandırmak için, denetimin `SelectMethod` özelliğini sayfanın kodundaki bir yöntem adına ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="b6093-139">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to a method name in the page's code.</span></span> <span data-ttu-id="b6093-140">Veri denetimi, yöntemi sayfa yaşam döngüsünde uygun zamanda çağırır ve döndürülen verileri otomatik olarak bağlar.</span><span class="sxs-lookup"><span data-stu-id="b6093-140">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="b6093-141">`DataBind` yöntemi açıkça çağrılmaya gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="b6093-141">There's no need to explicitly call the `DataBind` method.</span></span>

1. <span data-ttu-id="b6093-142">**Çözüm Gezgini**, *ProductList. aspx*' i açın.</span><span class="sxs-lookup"><span data-stu-id="b6093-142">In **Solution Explorer**, open *ProductList.aspx*.</span></span>
2. <span data-ttu-id="b6093-143">Var olan işaretlemeyi bu biçimlendirme ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b6093-143">Replace the existing markup with this markup:</span></span>   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="b6093-144">Bu kod, ürünleri göstermek için `productList` adlı bir **ListView** denetimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="b6093-144">This code uses a **ListView** control named `productList` to display products.</span></span>

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="b6093-145">Şablonlar ve stiller ile **ListView** denetiminin verileri nasıl görüntülediğini tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="b6093-145">With templates and styles, you define how the **ListView** control displays data.</span></span> <span data-ttu-id="b6093-146">Herhangi bir yinelenen yapıdaki veriler için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="b6093-146">It's useful for data in any repeating structure.</span></span> <span data-ttu-id="b6093-147">Bu **ListView** örneği yalnızca veritabanı verilerini görüntülüyor olsa da, kod olmadan, kullanıcıların verileri düzenlemesini, eklemesini ve silmesini ve verileri sıralama ve görüntüleme olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6093-147">Though this **ListView** example simply displays database data, you can also, without code, enable users to edit, insert, and delete data, and to sort and page data.</span></span>

<span data-ttu-id="b6093-148">**ListView** denetimindeki `ItemType` özelliğini ayarlayarak, veri bağlama ifadesi `Item` kullanılabilir ve denetimin türü kesin olarak belirlenmiş olur.</span><span class="sxs-lookup"><span data-stu-id="b6093-148">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="b6093-149">Önceki öğreticide belirtildiği gibi, `ProductName`belirtmek gibi IntelliSense ile öğe nesnesi ayrıntılarını seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b6093-149">As mentioned in the previous tutorial, you can select Item object details with IntelliSense, such as specifying the `ProductName`:</span></span>

![Veri öğelerini ve ayrıntıları görüntüleme-IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="b6093-151">Ayrıca, `SelectMethod` bir değer belirtmek için model bağlama de kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="b6093-151">You're also using model binding to specify a `SelectMethod` value.</span></span> <span data-ttu-id="b6093-152">Bu değer (`GetProducts`), sonraki adımda ürünlerin gösterilmesi için arka plandaki koda ekleyeceğiniz yönteme karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="b6093-152">This value (`GetProducts`) corresponds to the method you'll add to the code behind to display products in the next step.</span></span>

### <a name="add-code-to-display-products"></a><span data-ttu-id="b6093-153">Ürünleri göstermek için kod ekleme</span><span class="sxs-lookup"><span data-stu-id="b6093-153">Add code to display products</span></span>

<span data-ttu-id="b6093-154">Bu adımda, veritabanındaki ürün verileriyle **ListView** denetimini doldurmak için kod ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b6093-154">In this step, you'll add code to populate the **ListView** control with product data from the database.</span></span> <span data-ttu-id="b6093-155">Kod, tüm ürünlerin ve bireysel kategori ürünlerinin gösterilmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="b6093-155">The code supports showing all products and  individual category products.</span></span>

1. <span data-ttu-id="b6093-156">**Çözüm Gezgini**, *ProductList. aspx* öğesine sağ tıklayın ve ardından **kodu görüntüle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b6093-156">In **Solution Explorer**, right-click *ProductList.aspx* and then select **View Code**.</span></span>
2. <span data-ttu-id="b6093-157">*ProductList.aspx.cs* dosyasındaki mevcut kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b6093-157">Replace the existing code in the *ProductList.aspx.cs* file with this:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="b6093-158">Bu kod, **ListView** denetiminin `ItemType` özelliğinin *ProductList. aspx* sayfasında başvurduğu `GetProducts` yöntemini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6093-158">This code shows the `GetProducts` method that the **ListView** control's `ItemType` property references in the *ProductList.aspx* page.</span></span> <span data-ttu-id="b6093-159">Sonuçları belirli bir veritabanı kategorisiyle sınırlamak için, kod *ProductList. aspx* sayfasına gidildiği zaman *ProductList. aspx* sayfasına geçirilen sorgu dizesi değerindeki `categoryId` değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b6093-159">To limit the results to a specific database category, the code sets the `categoryId` value from the query string value passed to the *ProductList.aspx* page when the *ProductList.aspx* page is navigated to.</span></span> <span data-ttu-id="b6093-160">`System.Web.ModelBinding` ad alanındaki `QueryStringAttribute` sınıfı, `id`sorgu dizesi değişkeninin değerini almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b6093-160">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the value of the query string variable `id`.</span></span> <span data-ttu-id="b6093-161">Bu, model bağlamaya, sorgu dizesinden bir değeri, çalışma zamanında `categoryId` parametresine bağlamayı denemeye yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="b6093-161">This instructs model binding to try to bind a value from the query string to the `categoryId` parameter at run time.</span></span>

<span data-ttu-id="b6093-162">Geçerli bir kategori bir sorgu dizesi olarak sayfaya geçirildiğinde, sorgunun sonuçları, veritabanındaki `categoryId` değerle eşleşen bu ürünlerle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b6093-162">When a valid category is passed as a query string to the page, the results of the query are limited to those products in the database that match the `categoryId` value.</span></span> <span data-ttu-id="b6093-163">Örneğin, *Productslist. aspx* sayfası URL 'si ise:</span><span class="sxs-lookup"><span data-stu-id="b6093-163">For instance, if the *ProductsList.aspx* page URL is this:</span></span>

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="b6093-164">Sayfa yalnızca `categoryId` `1`eşit olan ürünleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b6093-164">The page displays only the products where the `categoryId` equals `1`.</span></span>

<span data-ttu-id="b6093-165">Tüm ürünler, *ProductList. aspx* sayfası çağrıldığında hiçbir sorgu dizesi dahil edilmediğinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b6093-165">All products are displayed if no query string is included when the *ProductList.aspx* page is called.</span></span>

<span data-ttu-id="b6093-166">Bu yöntemlere ait değer kaynakları, *değer sağlayıcıları* ( *QueryString*gibi) olarak adlandırılır ve kullanılacak değer sağlayıcısını belirten parametre öznitelikleri, *değer sağlayıcı öznitelikleri* (örneğin, `id`) olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="b6093-166">The sources of values for these methods are referred to as *value providers* (such as *QueryString*), and the parameter attributes that indicate which value provider to use are referred to as *value provider attributes* (such as `id`).</span></span> <span data-ttu-id="b6093-167">ASP.NET, sorgu dizesi, tanımlama bilgileri, form değerleri, denetimler, Görünüm durumu, oturum durumu ve profil özellikleri gibi Web Forms bir uygulamadaki tüm tipik Kullanıcı girişi kaynakları için değer sağlayıcıları ve karşılık gelen öznitelikler içerir.</span><span class="sxs-lookup"><span data-stu-id="b6093-167">ASP.NET includes value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="b6093-168">Ayrıca, özel değer sağlayıcıları yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6093-168">You can also write custom value providers.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="b6093-169">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b6093-169">Run the application</span></span>

<span data-ttu-id="b6093-170">Tüm ürünleri veya bir kategorinin ürünlerini görüntülemek için uygulamayı şimdi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b6093-170">Run the application now to view all products or a category's products.</span></span>

1. <span data-ttu-id="b6093-171">Uygulamayı çalıştırmak için Visual Studio 'da **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="b6093-171">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="b6093-172">Tarayıcı açılır ve *default. aspx* sayfasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6093-172">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="b6093-173">Ürün kategorisi gezinti menüsünden **otomobilleri** seçin.</span><span class="sxs-lookup"><span data-stu-id="b6093-173">Select **Cars** from the product category navigation menu.</span></span>  
   <span data-ttu-id="b6093-174">*ProductList. aspx* sayfası yalnızca **araba** kategorisi ürünlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6093-174">The *ProductList.aspx* page displays showing only **Cars** category products.</span></span> <span data-ttu-id="b6093-175">Bu öğreticide daha sonra ürün ayrıntıları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b6093-175">Later in this tutorial, you'll display product details.</span></span>  

    ![Veri öğelerini ve ayrıntılarını görüntüleme-otomobiller](display_data_items_and_details/_static/image2.png)

3. <span data-ttu-id="b6093-177">Üstteki gezinti menüsünden **Ürünler** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="b6093-177">Select **Products** from the navigation menu at the top.</span></span>  
   <span data-ttu-id="b6093-178">Ayrıca, *ProductList. aspx* sayfası görüntülenir, ancak bu kez tüm ürün listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6093-178">Again, the *ProductList.aspx* page is displayed, however this time it shows the entire list of products.</span></span>   

    ![Veri öğelerini ve ayrıntıları görüntüleme-ürünler](display_data_items_and_details/_static/image3.png)

4. <span data-ttu-id="b6093-180">Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="b6093-180">Close the browser and return to Visual Studio.</span></span>

### <a name="add-a-data-control-to-display-product-details"></a><span data-ttu-id="b6093-181">Ürün ayrıntılarını göstermek için bir veri denetimi ekleyin</span><span class="sxs-lookup"><span data-stu-id="b6093-181">Add a data control to display product details</span></span>

<span data-ttu-id="b6093-182">Daha sonra, belirli ürün bilgilerini göstermek için önceki öğreticide eklediğiniz *ProductDetails. aspx* sayfasındaki biçimlendirmeyi değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b6093-182">Next, you'll modify the markup in the *ProductDetails.aspx* page that you added in the previous tutorial to display specific product information.</span></span>

1. <span data-ttu-id="b6093-183">**Çözüm Gezgini**' de *ProductDetails. aspx*' i açın.</span><span class="sxs-lookup"><span data-stu-id="b6093-183">In **Solution Explorer**, open *ProductDetails.aspx*.</span></span>

2. <span data-ttu-id="b6093-184">Var olan işaretlemeyi bu biçimlendirme ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b6093-184">Replace the existing markup with this markup:</span></span>

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    <span data-ttu-id="b6093-185">Bu kod, belirli ürün ayrıntılarını göstermek için bir **FormView** denetimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="b6093-185">This code uses a **FormView** control to display specific product details.</span></span> <span data-ttu-id="b6093-186">Bu biçimlendirme, *ProductList. aspx* sayfasında verileri göstermek için kullanılan yöntemler gibi yöntemleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="b6093-186">This markup uses methods like the methods used to display data in the *ProductList.aspx* page.</span></span> <span data-ttu-id="b6093-187">**FormView** denetimi, bir veri kaynağından tek seferde tek bir kayıt göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b6093-187">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="b6093-188">**FormView** denetimini kullandığınızda, veri bağlantılı değerleri göstermek ve düzenlemek için şablonlar oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="b6093-188">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="b6093-189">Bu şablonlar denetimleri, bağlama ifadelerini ve formun görünümünü ve işlevselliğini tanımlayan biçimlendirmeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="b6093-189">These templates contain controls, binding expressions, and formatting that define the form's look and functionality.</span></span>

<span data-ttu-id="b6093-190">Önceki biçimlendirmeyi veritabanına bağlamak ek kod gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b6093-190">Connecting the previous markup to the database requires additional code.</span></span>

1. <span data-ttu-id="b6093-191">**Çözüm Gezgini**, *ProductDetails. aspx* öğesine sağ tıklayın ve ardından **kodu görüntüle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6093-191">In **Solution Explorer**, right-click *ProductDetails.aspx* and then click **View Code**.</span></span>  
   <span data-ttu-id="b6093-192">*ProductDetails.aspx.cs* dosyası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b6093-192">The *ProductDetails.aspx.cs* file is displayed.</span></span>

2. <span data-ttu-id="b6093-193">Mevcut kodu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b6093-193">Replace the existing code with this code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="b6093-194">Bu kod, bir "`productID`" sorgu dizesi değeri olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="b6093-194">This code checks for a "`productID`" query-string value.</span></span> <span data-ttu-id="b6093-195">Geçerli bir sorgu dizesi değeri bulunursa, eşleşen ürün görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b6093-195">If a valid query-string value is found, the matching product is displayed.</span></span> <span data-ttu-id="b6093-196">Sorgu dizesi bulunmazsa veya değeri geçerli değilse, ürün gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="b6093-196">If the query-string isn't found, or its value isn't valid, no product is displayed.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="b6093-197">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b6093-197">Run the application</span></span>

<span data-ttu-id="b6093-198">Artık, ürün KIMLIĞI temelinde bir ürünün görüntülendiğini görmek için uygulamayı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6093-198">Now you can run the application to see an individual product displayed based on product ID.</span></span>

1. <span data-ttu-id="b6093-199">Uygulamayı çalıştırmak için Visual Studio 'da **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="b6093-199">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="b6093-200">Tarayıcı açılır ve *default. aspx* sayfasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6093-200">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="b6093-201">Kategori gezinti menüsünden **Boats** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b6093-201">Select **Boats** from the category navigation menu.</span></span>  
   <span data-ttu-id="b6093-202">*ProductList. aspx* sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b6093-202">The *ProductList.aspx* page is displayed.</span></span>

3. <span data-ttu-id="b6093-203">Ürün listesinden **Kağıt bot** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b6093-203">Select **Paper Boat** from the product list.</span></span>
   <span data-ttu-id="b6093-204">*ProductDetails. aspx* sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b6093-204">The *ProductDetails.aspx* page is displayed.</span></span>

    ![Veri öğelerini ve ayrıntıları görüntüleme-ürünler](display_data_items_and_details/_static/image4.png)
    
4. <span data-ttu-id="b6093-206">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="b6093-206">Close the browser.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b6093-207">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b6093-207">Additional resources</span></span>

[<span data-ttu-id="b6093-208">Model bağlama ve Web formları ile verileri alma ve görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b6093-208">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a><span data-ttu-id="b6093-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b6093-209">Next steps</span></span>

<span data-ttu-id="b6093-210">Bu öğreticide, ürünleri ve ürün ayrıntılarını göstermek için biçimlendirme ve kod eklediniz.</span><span class="sxs-lookup"><span data-stu-id="b6093-210">In this tutorial, you added markup and code to display products and product details.</span></span> <span data-ttu-id="b6093-211">Kesin tür belirtilmiş veri denetimleri, model bağlama ve değer sağlayıcıları hakkında bilgi edindiniz.</span><span class="sxs-lookup"><span data-stu-id="b6093-211">You learned about strongly typed data controls, model binding, and value providers.</span></span> <span data-ttu-id="b6093-212">Sonraki öğreticide, Wingtip Toys örnek uygulamasına bir alışveriş sepeti ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b6093-212">In the next tutorial, you'll add a shopping cart to the Wingtip Toys sample application.</span></span> 

> [!div class="step-by-step"]
> <span data-ttu-id="b6093-213">[Önceki](ui_and_navigation.md)
> [İleri](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="b6093-213">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
