---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: '4\. Bölüm: ürünleri listeleme | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 4\. bölüm, GridView contenr ile ürünleri listelemeyi içerir...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566985"
---
# <a name="part-4-listing-products"></a><span data-ttu-id="d9f2b-104">4\. Bölüm: Ürünleri Listeleme</span><span class="sxs-lookup"><span data-stu-id="d9f2b-104">Part 4: Listing Products</span></span>

<span data-ttu-id="d9f2b-105">[ali Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="d9f2b-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="d9f2b-106">Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="d9f2b-107">Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="d9f2b-108">Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="d9f2b-109">4\. bölüm, GridView denetimiyle ürünlerin dökümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-109">Part 4 covers listing products with the GridView control.</span></span>

## <a id="_Toc260221670"></a><span data-ttu-id="d9f2b-110">GridView denetimiyle ürünleri listeleme</span><span class="sxs-lookup"><span data-stu-id="d9f2b-110">Listing Products with the GridView Control</span></span>

<span data-ttu-id="d9f2b-111">Çözümünüzde "sağ tıklayıp" "Ekle" ve "yeni öğe" seçeneğini belirleyerek ProductsList. aspx sayfamızı uygulamaya başlayalım.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-111">Let's begin implementing our ProductsList.aspx page by "Right Clicking" on our solution and selecting "Add" and "New Item".</span></span>

![](tailspin-spyworks-part-4/_static/image1.jpg)

<span data-ttu-id="d9f2b-112">"Ana sayfa kullanarak Web formu" seçeneğini belirleyin ve ProductsList. aspx "bir sayfa adı girin.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-112">Choose "Web Form Using Master Page" and enter a page name of ProductsList.aspx".</span></span>

<span data-ttu-id="d9f2b-113">"Ekle" ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-113">Click "Add".</span></span>

![](tailspin-spyworks-part-4/_static/image2.jpg)

<span data-ttu-id="d9f2b-114">Ardından, site. Master sayfasını yerleştirdiğiniz "stiller" klasörünü seçin ve "klasör Içeriği" penceresinden seçin.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-114">Next choose the "Styles" folder where we placed the Site.Master page and select it from the "Contents of folder" window.</span></span>

![](tailspin-spyworks-part-4/_static/image3.jpg)

<span data-ttu-id="d9f2b-115">Sayfayı oluşturmak için "Tamam" a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-115">Click "Ok" to create the page.</span></span>

<span data-ttu-id="d9f2b-116">Veritabanımız aşağıda görüldüğü gibi ürün verileriyle doldurulmuştur.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-116">Our database is populated with product data as seen below.</span></span>

![](tailspin-spyworks-part-4/_static/image4.jpg)

<span data-ttu-id="d9f2b-117">Sayfanız oluşturulduktan sonra, bu ürün verilerine erişmek için bir varlık veri kaynağı kullanacağız, ancak bu örnekte ürün varlıklarını seçmemiz gerekir ve döndürülen öğeleri yalnızca seçili kategoriye ait olanlarla kısıtlayacağız.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-117">After our page is created we'll again use an Entity Data Source to access that product data, but in this instance we need to select the Product Entities and we need to restrict the items that are returned to only those for the selected Category.</span></span>

<span data-ttu-id="d9f2b-118">Bunu gerçekleştirmek için, EntityDataSource 'un WHERE yan tümcesini otomatik olarak oluşturmasını söyleyecektir ve WHERE parametresini belirteceğiz.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-118">To accomplish this we'll tell the EntityDataSource to Auto Generate the WHERE clause and we'll specify the WhereParameter.</span></span>

<span data-ttu-id="d9f2b-119">"Ürün kategorisi menüsündeki" menü öğelerini oluşturduğumuzda bu bağlantıyı, her bir bağlantı için QueryString öğesine CategoryID ekleyerek dinamik olarak oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-119">You'll recall that when we created the Menu Items in our "Product Category Menu" we dynamically built the link by adding the CategoryID to the QueryString for each link.</span></span> <span data-ttu-id="d9f2b-120">Varlık veri kaynağına, bu QueryString parametresinden WHERE parametresini türetmesini söylüreceğiz.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-120">We will tell the Entity Data Source to derive the WHERE parameter from that QueryString parameter.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

<span data-ttu-id="d9f2b-121">Daha sonra, ListView denetimini ürünlerin bir listesini görüntüleyecek şekilde yapılandıracağız.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-121">Next, we'll configure the ListView control to display a list of products.</span></span> <span data-ttu-id="d9f2b-122">En iyi bir alışveriş deneyimi oluşturmak için, ListVew 'imizde görüntülenecek olan her bir ürüne yönelik birkaç kısa özelliği sıkıştıracağız.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-122">To create an optimal shopping experience we'll compact several concise features into each individual product displayed in our ListVew.</span></span>

- <span data-ttu-id="d9f2b-123">Ürün adı ürünün ayrıntı görünümünün bir bağlantısı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-123">The product name will be a link to the product's detail view.</span></span>
- <span data-ttu-id="d9f2b-124">Ürünün fiyatı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-124">The product's price will be displayed.</span></span>
- <span data-ttu-id="d9f2b-125">Ürünün bir görüntüsü görüntülenir ve uygulamamızda bir katalog görüntüleri dizininden görüntüyü dinamik olarak seçeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-125">An image of the product will be displayed and we'll dynamically select the image from a catalog images directory in our application.</span></span>
- <span data-ttu-id="d9f2b-126">Belirli ürünü, alışveriş sepetine hemen eklemek için bir bağlantı ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-126">We will include a link to immediately add the specific product to the shopping cart.</span></span>

<span data-ttu-id="d9f2b-127">ListView denetim örneğimiz için biçimlendirme aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-127">Here is the markup for our ListView control instance.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

<span data-ttu-id="d9f2b-128">Görüntülenen her ürün için birçok bağlantı dinamik olarak derleniyor.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-128">We are dynamically building several links for each displayed product.</span></span>

<span data-ttu-id="d9f2b-129">Ayrıca, yeni sayfayı test etmeden önce, ürün kataloğu görüntülerinin dizin yapısını aşağıda gösterildiği gibi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-129">Also, before we test own new page we need to create the directory structure for the product catalog images as follows.</span></span>

![](tailspin-spyworks-part-4/_static/image1.png)

<span data-ttu-id="d9f2b-130">Ürün görüntülerimizin erişilebilir olması, ürün listesi sayfamızı test edebilir.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-130">Once our product images are accessible we can test our product list page.</span></span>

![](tailspin-spyworks-part-4/_static/image5.jpg)

<span data-ttu-id="d9f2b-131">Sitenin giriş sayfasından kategori listesi bağlantılarından birine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-131">From the site's home page, click on one of the Category List Links.</span></span>

![](tailspin-spyworks-part-4/_static/image6.jpg)

<span data-ttu-id="d9f2b-132">Şimdi ProductDetails. aspx sayfasını ve AddToCart işlevini uygulamamız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-132">Now we need to implement the ProductDetails.aspx page and the AddToCart functionality.</span></span>

<span data-ttu-id="d9f2b-133">Daha önce yaptığımız gibi, site ana sayfasını kullanarak ProductDetails. aspx adlı bir sayfa adı oluşturmak için File-New&gt;kullanın.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-133">Use File-&gt;New to create a page name ProductDetails.aspx using the site Master Page as we did previously.</span></span>

<span data-ttu-id="d9f2b-134">Veritabanında belirli ürün kaydına erişmek için bir EntityDataSource denetimi kullanacağız ve ürün verilerini aşağıdaki gibi göstermek için bir ASP.NET FormView denetimi kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-134">We will again use an EntityDataSource control to access the specific product record in the database and we will use an ASP.NET FormView control to display the product data as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

<span data-ttu-id="d9f2b-135">Biçimlendirme biraz komik bir şekilde görünüyorsa endişelenmeyin.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-135">Don't worry if the formatting looks a bit funny to you.</span></span> <span data-ttu-id="d9f2b-136">Yukarıdaki biçimlendirme, daha sonra uygulayacağımız birkaç özellik için görüntü düzeninde yer bırakır.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-136">The markup above leaves room in the display layout for a couple of features we'll implement later on.</span></span>

<span data-ttu-id="d9f2b-137">Alışveriş sepeti, uygulamamızda daha karmaşık mantığı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-137">The Shopping Cart will represent the more complex logic in our application.</span></span> <span data-ttu-id="d9f2b-138">Başlamak için File-&gt;New ' i kullanarak MyShoppingCart. aspx adlı bir sayfa oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-138">To get started, use File-&gt;New to create a page called MyShoppingCart.aspx.</span></span>

<span data-ttu-id="d9f2b-139">ShoppingCart. aspx adını seçmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-139">Note that we are not choosing the name ShoppingCart.aspx.</span></span>

<span data-ttu-id="d9f2b-140">Veritabanımız "ShoppingCart" adlı bir tablo içeriyor.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-140">Our database contains a table named "ShoppingCart".</span></span> <span data-ttu-id="d9f2b-141">Bir Varlık Veri Modeli oluşturduğumuz veritabanındaki her tablo için bir sınıf oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-141">When we generated an Entity Data Model a class was created for each table in the database.</span></span> <span data-ttu-id="d9f2b-142">Bu nedenle Varlık Veri Modeli, "ShoppingCart" adlı bir varlık sınıfı oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-142">Therefore, the Entity Data Model generated an Entity Class named "ShoppingCart".</span></span> <span data-ttu-id="d9f2b-143">Modeli, alışveriş sepeti uygulamamız için bu adı kullanabilmemiz veya gereksinimlerinize göre uzatmamız için düzenleyebiliriz, ancak çakışmayı önlemek için yalnızca bir ad seçmek yerine kabul edeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-143">We could edit the model so that we could use that name for our shopping cart implementation or extend it for our needs, but we will opt instead to simply select a name that will avoid the conflict.</span></span>

<span data-ttu-id="d9f2b-144">Ayrıca, bir basit alışveriş sepeti oluşturmak ve alışveriş sepeti gösterimi ile alışveriş sepeti mantığını katıştırmak için de dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-144">It's also worth noting that we will be creating a simple shopping cart and embedding the shopping cart logic with the shopping cart display.</span></span> <span data-ttu-id="d9f2b-145">Ayrıca, alışveriş sepetimizi tamamen ayrı bir Iş katmanında uygulamayı da tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9f2b-145">We might also choose to implement our shopping cart in a completely separate Business Layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d9f2b-146">[Önceki](tailspin-spyworks-part-3.md)
> [İleri](tailspin-spyworks-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="d9f2b-146">[Previous](tailspin-spyworks-part-3.md)
[Next](tailspin-spyworks-part-5.md)</span></span>
