---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: '8\. kısım: Ajax güncelleştirmeleriyle alışveriş sepeti | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 5\. bölüm, Ajax güncelleştirmeleriyle alışveriş sepetini içerir.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539258"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a><span data-ttu-id="76547-104">8\. Bölüm: Ajax Güncelleştirmeleriyle Alışveriş Sepeti</span><span class="sxs-lookup"><span data-stu-id="76547-104">Part 8: Shopping Cart with Ajax Updates</span></span>

<span data-ttu-id="76547-105">[Jon Galloway](https://github.com/jongalloway) tarafından</span><span class="sxs-lookup"><span data-stu-id="76547-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="76547-106">MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="76547-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="76547-107">MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="76547-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="76547-108">Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="76547-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="76547-109">5\. bölüm, Ajax güncelleştirmeleriyle alışveriş sepetini içerir.</span><span class="sxs-lookup"><span data-stu-id="76547-109">Part 8 covers Shopping Cart with Ajax Updates.</span></span>

<span data-ttu-id="76547-110">Kullanıcıların, kayıt yaptırmadan albümleri sepetlerine yerleştirmelerini sağlar, ancak kullanıma alma işlemini tamamlaması için konuk olarak kaydolmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="76547-110">We'll allow users to place albums in their cart without registering, but they'll need to register as guests to complete checkout.</span></span> <span data-ttu-id="76547-111">Alışveriş ve kullanıma alma işlemi iki denetleyicide ayrılacaktır: bir alışveriş sepeti denetleyicisi ve bu, kullanıma alma işlemini işleyen bir kullanıma alma denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="76547-111">The shopping and checkout process will be separated into two controllers: a ShoppingCart Controller which allows anonymously adding items to a cart, and a Checkout Controller which handles the checkout process.</span></span> <span data-ttu-id="76547-112">Bu bölümdeki alışveriş sepetini kullanmaya başlayacağız, ardından aşağıdaki bölümde kullanıma alma işlemini oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="76547-112">We'll start with the Shopping Cart in this section, then build the Checkout process in the following section.</span></span>

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a><span data-ttu-id="76547-113">Sepet, sipariş ve OrderDetail model sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="76547-113">Adding the Cart, Order, and OrderDetail model classes</span></span>

<span data-ttu-id="76547-114">Alışveriş sepetimiz ve kullanıma alma işlemlerimiz bazı yeni sınıfların kullanımını sağlayacak.</span><span class="sxs-lookup"><span data-stu-id="76547-114">Our Shopping Cart and Checkout processes will make use of some new classes.</span></span> <span data-ttu-id="76547-115">Modeller klasörüne sağ tıklayın ve aşağıdaki kodla bir sepet sınıfı (Cart.cs) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="76547-115">Right-click the Models folder and add a Cart class (Cart.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

<span data-ttu-id="76547-116">Bu sınıf, şu ana kadar kullandığımız diğerlerine, recordID özelliği için [key] özniteliği dışında oldukça benzer.</span><span class="sxs-lookup"><span data-stu-id="76547-116">This class is pretty similar to others we've used so far, with the exception of the [Key] attribute for the RecordId property.</span></span> <span data-ttu-id="76547-117">Sepet öğelerimiz, adsız alışverişe izin vermek için CartId adlı bir dize tanımlayıcısına sahip olacaktır, ancak tablo, recordID adlı bir tamsayı birincil anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="76547-117">Our Cart items will have a string identifier named CartID to allow anonymous shopping, but the table includes an integer primary key named RecordId.</span></span> <span data-ttu-id="76547-118">Kural gereği, Entity Framework kodu-önce sepet adlı bir tablonun birincil anahtarının CartId veya ID olacağını bekler, ancak bunu yapmak isterseniz ek açıklamalar veya kod aracılığıyla kolayca geçersiz kılabiliriz.</span><span class="sxs-lookup"><span data-stu-id="76547-118">By convention, Entity Framework Code-First expects that the primary key for a table named Cart will be either CartId or ID, but we can easily override that via annotations or code if we want.</span></span> <span data-ttu-id="76547-119">Bu, Entity Framework kodda basit kuralları nasıl kullanabileceğimizi gösteren bir örnektir, ancak bu, ne zaman bir kez karşılaştıklarında bunlarla sınırlandırılıyoruz.</span><span class="sxs-lookup"><span data-stu-id="76547-119">This is an example of how we can use the simple conventions in Entity Framework Code-First when they suit us, but we're not constrained by them when they don't.</span></span>

<span data-ttu-id="76547-120">Ardından, aşağıdaki kodla bir order class (Order.cs) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="76547-120">Next, add an Order class (Order.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

<span data-ttu-id="76547-121">Bu sınıf, bir sipariş için Özet ve teslim bilgilerini izler.</span><span class="sxs-lookup"><span data-stu-id="76547-121">This class tracks summary and delivery information for an order.</span></span> <span data-ttu-id="76547-122">Henüz oluşturulamadığımız bir sınıfa bağlı olan bir OrderDetails gezinti özelliği olduğundan, **henüz derlenmez**.</span><span class="sxs-lookup"><span data-stu-id="76547-122">**It won't compile yet**, because it has an OrderDetails navigation property which depends on a class we haven't created yet.</span></span> <span data-ttu-id="76547-123">Şimdi, aşağıdaki kodu ekleyerek OrderDetail.cs adlı bir sınıf ekleyerek bunu düzeldelim.</span><span class="sxs-lookup"><span data-stu-id="76547-123">Let's fix that now by adding a class named OrderDetail.cs, adding the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

<span data-ttu-id="76547-124">Bir DbSet&lt;sanatçı&gt;de dahil olmak üzere, bu yeni model sınıflarını sunan DbSets 'leri dahil etmek için MusicStoreEntities sınıfımız son bir güncelleştirme yapacağız.</span><span class="sxs-lookup"><span data-stu-id="76547-124">We'll make one last update to our MusicStoreEntities class to include DbSets which expose those new Model classes, also including a DbSet&lt;Artist&gt;.</span></span> <span data-ttu-id="76547-125">Güncelleştirilmiş MusicStoreEntities sınıfı aşağıda gösterildiği gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="76547-125">The updated MusicStoreEntities class appears as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="76547-126">Alışveriş sepetini iş mantığını yönetme</span><span class="sxs-lookup"><span data-stu-id="76547-126">Managing the Shopping Cart business logic</span></span>

<span data-ttu-id="76547-127">Daha sonra, modeller klasöründe ShoppingCart sınıfını oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="76547-127">Next, we'll create the ShoppingCart class in the Models folder.</span></span> <span data-ttu-id="76547-128">ShoppingCart modeli, sepet tablosuna veri erişimini işler.</span><span class="sxs-lookup"><span data-stu-id="76547-128">The ShoppingCart model handles data access to the Cart table.</span></span> <span data-ttu-id="76547-129">Ayrıca, alışveriş sepetinden öğe ekleme ve kaldırma için iş mantığını işleymeyecektir.</span><span class="sxs-lookup"><span data-stu-id="76547-129">Additionally, it will handle the business logic to for adding and removing items from the shopping cart.</span></span>

<span data-ttu-id="76547-130">Kullanıcıların alışveriş sepetine öğe eklemek için bir hesaba kaydolmaları gerektirmek istediğimiz için, alışveriş sepetine erişirken kullanıcılara geçici bir benzersiz tanımlayıcı (GUID veya genel benzersiz tanımlayıcı kullanarak) atayacağız.</span><span class="sxs-lookup"><span data-stu-id="76547-130">Since we don't want to require users to sign up for an account just to add items to their shopping cart, we will assign users a temporary unique identifier (using a GUID, or globally unique identifier) when they access the shopping cart.</span></span> <span data-ttu-id="76547-131">Bu KIMLIĞI ASP.NET oturum sınıfını kullanarak depolayacağız.</span><span class="sxs-lookup"><span data-stu-id="76547-131">We'll store this ID using the ASP.NET Session class.</span></span>

<span data-ttu-id="76547-132">*Note: ASP.NET oturumu, siteye ayrıldıktan sonra sona ereceği kullanıcıya özgü bilgileri depolamak için uygun bir yerdir. Oturum durumunun kötüye kullanımı daha büyük sitelerde performans etkilerine sahip olsa da, hafif kullanım, tanıtım amacıyla iyi bir şekilde çalışacaktır.*</span><span class="sxs-lookup"><span data-stu-id="76547-132">*Note: The ASP.NET Session is a convenient place to store user-specific information which will expire after they leave the site. While misuse of session state can have performance implications on larger sites, our light use will work well for demonstration purposes.*</span></span>

<span data-ttu-id="76547-133">ShoppingCart sınıfı aşağıdaki yöntemleri kullanıma sunar:</span><span class="sxs-lookup"><span data-stu-id="76547-133">The ShoppingCart class exposes the following methods:</span></span>

<span data-ttu-id="76547-134">**AddToCart** bir albümü parametre olarak alır ve kullanıcının sepetine ekler.</span><span class="sxs-lookup"><span data-stu-id="76547-134">**AddToCart** takes an Album as a parameter and adds it to the user's cart.</span></span> <span data-ttu-id="76547-135">Sepet tablosu her bir albümün miktarını izlediğinden, gerektiğinde yeni bir satır oluşturma veya Kullanıcı zaten bir albümün kopyasını sipariş eden miktarı artırma mantığını içerir.</span><span class="sxs-lookup"><span data-stu-id="76547-135">Since the Cart table tracks quantity for each album, it includes logic to create a new row if needed or just increment the quantity if the user has already ordered one copy of the album.</span></span>

<span data-ttu-id="76547-136">**Removefromcart** BIR albüm kimliği alır ve kullanıcının sepetinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="76547-136">**RemoveFromCart** takes an Album ID and removes it from the user's cart.</span></span> <span data-ttu-id="76547-137">Kullanıcının sepetine yalnızca bir albümün kopyası varsa, satır kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="76547-137">If the user only had one copy of the album in their cart, the row is removed.</span></span>

<span data-ttu-id="76547-138">**Emptycart** bir kullanıcının alışveriş sepetinden tüm öğeleri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="76547-138">**EmptyCart** removes all items from a user's shopping cart.</span></span>

<span data-ttu-id="76547-139">**Getcartıtems** , ekran veya Işleme Için cartıtems listesini alır.</span><span class="sxs-lookup"><span data-stu-id="76547-139">**GetCartItems** retrieves a list of CartItems for display or processing.</span></span>

<span data-ttu-id="76547-140">**GetCount** , bir kullanıcının alışveriş sepetindeki toplam albüm sayısını alır.</span><span class="sxs-lookup"><span data-stu-id="76547-140">**GetCount** retrieves a the total number of albums a user has in their shopping cart.</span></span>

<span data-ttu-id="76547-141">**Gettotal** , sepetteki tüm öğelerin toplam maliyetini hesaplar.</span><span class="sxs-lookup"><span data-stu-id="76547-141">**GetTotal** calculates the total cost of all items in the cart.</span></span>

<span data-ttu-id="76547-142">**CreateOrder** , alışveriş sepetini, kullanıma alma aşamasında bir sıraya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="76547-142">**CreateOrder** converts the shopping cart to an order during the checkout phase.</span></span>

<span data-ttu-id="76547-143">**Getcart** , denetleyicilerimizin bir sepet nesnesi elde etmesine olanak tanıyan statik bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="76547-143">**GetCart** is a static method which allows our controllers to obtain a cart object.</span></span> <span data-ttu-id="76547-144">Kullanıcının oturumundan CartId 'yi okumayı işlemek için **Getcartıd** yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="76547-144">It uses the **GetCartId** method to handle reading the CartId from the user's session.</span></span> <span data-ttu-id="76547-145">Getcartıd yöntemi, kullanıcının oturumunun kullanıcı oturumundan okuyabilmesi için HttpContextBase 'i gerektirir.</span><span class="sxs-lookup"><span data-stu-id="76547-145">The GetCartId method requires the HttpContextBase so that it can read the user's CartId from user's session.</span></span>

<span data-ttu-id="76547-146">Aşağıda, tüm **ShoppingCart sınıfı**verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="76547-146">Here's the complete **ShoppingCart class**:</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a><span data-ttu-id="76547-147">ViewModel 'lar</span><span class="sxs-lookup"><span data-stu-id="76547-147">ViewModels</span></span>

<span data-ttu-id="76547-148">Alışveriş sepeti denetleyicinizin, bazı karmaşık bilgileri, model nesnelerimize düzgün bir şekilde eşlenmeyen görünümlerimize iletmelerini gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="76547-148">Our Shopping Cart Controller will need to communicate some complex information to its views which doesn't map cleanly to our Model objects.</span></span> <span data-ttu-id="76547-149">Modellerimizi görünümlerimize uyacak şekilde değiştirmek istemiyorum; Model sınıfları kullanıcı arabirimini değil, etki alanını temsil etmelidir.</span><span class="sxs-lookup"><span data-stu-id="76547-149">We don't want to modify our Models to suit our views; Model classes should represent our domain, not the user interface.</span></span> <span data-ttu-id="76547-150">Tek bir çözüm, mağaza yöneticisi açılan bilgileriyle yaptığımız gibi, ViewBag sınıfını kullanarak bu bilgileri görünümlerimize geçirmektir, ancak ViewBag aracılığıyla çok fazla bilgi geçirilerek yönetimi zor olur.</span><span class="sxs-lookup"><span data-stu-id="76547-150">One solution would be to pass the information to our Views using the ViewBag class, as we did with the Store Manager dropdown information, but passing a lot of information via ViewBag gets hard to manage.</span></span>

<span data-ttu-id="76547-151">Bu, *ViewModel* deseninin kullanıldığı bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="76547-151">A solution to this is to use the *ViewModel* pattern.</span></span> <span data-ttu-id="76547-152">Bu model kullanılırken, belirli görünüm senaryolarımız için optimize edilmiş ve görünüm şablonlarımız tarafından gerek duyulan dinamik değerler/içerik özelliklerini sunan kesin türü belirtilmiş sınıflar oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="76547-152">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="76547-153">Denetleyici sınıflarımız daha sonra bu görünümün en iyi duruma getirilmiş sınıflarını, kullanılacak görünüm şablonumuza yerleştirebilir ve geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="76547-153">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="76547-154">Bu, Görünüm şablonları içinde tür güvenliği, derleme zamanı denetimi ve düzenleyici IntelliSense 'i sunar.</span><span class="sxs-lookup"><span data-stu-id="76547-154">This enables type-safety, compile-time checking, and editor IntelliSense within view templates.</span></span>

<span data-ttu-id="76547-155">Alışveriş sepeti denetleyicimizde kullanılmak üzere iki görünüm modeli oluşturacağız: ShoppingCartViewModel kullanıcının alışveriş sepetinin içeriğini tutacağından, bir Kullanıcı bir şeyi kaldırdığında bir sorun çıkardığında, ShoppingCartRemoveViewModel, onay bilgilerini görüntülemek için kullanılacaktır , sepetlerinden.</span><span class="sxs-lookup"><span data-stu-id="76547-155">We'll create two View Models for use in our Shopping Cart controller: the ShoppingCartViewModel will hold the contents of the user's shopping cart, and the ShoppingCartRemoveViewModel will be used to display confirmation information when a user removes something from their cart.</span></span>

<span data-ttu-id="76547-156">İşleri düzenli tutmak için projemizin ' ın kökünde yeni bir Viewmodeller klasörü oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="76547-156">Let's create a new ViewModels folder in the root of our project to keep things organized.</span></span> <span data-ttu-id="76547-157">Projeye sağ tıklayın, Ekle/yeni klasör ' ü seçin.</span><span class="sxs-lookup"><span data-stu-id="76547-157">Right-click the project, select Add / New Folder.</span></span>

![](mvc-music-store-part-8/_static/image1.jpg)

<span data-ttu-id="76547-158">Klasör Viewmodellerini adlandırın.</span><span class="sxs-lookup"><span data-stu-id="76547-158">Name the folder ViewModels.</span></span>

![](mvc-music-store-part-8/_static/image1.png)

<span data-ttu-id="76547-159">Ardından, Viewmodeller klasörüne ShoppingCartViewModel sınıfını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="76547-159">Next, add the ShoppingCartViewModel class in the ViewModels folder.</span></span> <span data-ttu-id="76547-160">İki özelliğe sahiptir: sepet öğelerinin listesi ve sepetteki tüm öğelerin toplam fiyatını tutacak bir ondalık değer.</span><span class="sxs-lookup"><span data-stu-id="76547-160">It has two properties: a list of Cart items, and a decimal value to hold the total price for all items in the cart.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

<span data-ttu-id="76547-161">Şimdi, aşağıdaki dört özellik ile ShoppingCartRemoveViewModel ' i Viewmodeller klasörüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="76547-161">Now add the ShoppingCartRemoveViewModel to the ViewModels folder, with the following four properties.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a><span data-ttu-id="76547-162">Alışveriş sepeti denetleyicisi</span><span class="sxs-lookup"><span data-stu-id="76547-162">The Shopping Cart Controller</span></span>

<span data-ttu-id="76547-163">Alışveriş sepeti denetleyicisi üç ana amaca sahiptir: bir sepete öğe ekleme, sepetten öğe kaldırma ve sepetteki öğeleri görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="76547-163">The Shopping Cart controller has three main purposes: adding items to a cart, removing items from the cart, and viewing items in the cart.</span></span> <span data-ttu-id="76547-164">Yeni oluşturduğumuz üç sınıfı kullanacaktır: ShoppingCartViewModel, ShoppingCartRemoveViewModel ve ShoppingCart.</span><span class="sxs-lookup"><span data-stu-id="76547-164">It will make use of the three classes we just created: ShoppingCartViewModel, ShoppingCartRemoveViewModel, and ShoppingCart.</span></span> <span data-ttu-id="76547-165">StoreController ve StoreManagerController 'da olduğu gibi, MusicStoreEntities 'in bir örneğini tutmak için bir alan ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="76547-165">As in the StoreController and StoreManagerController, we'll add a field to hold an instance of MusicStoreEntities.</span></span>

<span data-ttu-id="76547-166">Boş denetleyici şablonunu kullanarak projeye yeni bir alışveriş sepeti denetleyicisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="76547-166">Add a new Shopping Cart controller to the project using the Empty controller template.</span></span>

![](mvc-music-store-part-8/_static/image2.png)

<span data-ttu-id="76547-167">İşte bu, tüm ShoppingCart denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="76547-167">Here's the complete ShoppingCart Controller.</span></span> <span data-ttu-id="76547-168">Dizin ve ekleme denetleyicisi eylemleri çok tanıdık görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="76547-168">The Index and Add Controller actions should look very familiar.</span></span> <span data-ttu-id="76547-169">Remove ve CartSummary denetleyici eylemleri, aşağıdaki bölümde ele alacağız iki özel durumu ele alır.</span><span class="sxs-lookup"><span data-stu-id="76547-169">The Remove and CartSummary controller actions handle two special cases, which we'll discuss in the following section.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a><span data-ttu-id="76547-170">JQuery ile Ajax güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="76547-170">Ajax Updates with jQuery</span></span>

<span data-ttu-id="76547-171">Daha sonra, ShoppingCartViewModel için kesin olarak belirlenmiş bir alışveriş sepeti Dizin sayfası oluşturacak ve daha önce ile aynı yöntemi kullanarak liste görünümü şablonunu kullanıyor olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="76547-171">We'll next create a Shopping Cart Index page that is strongly typed to the ShoppingCartViewModel and uses the List View template using the same method as before.</span></span>

![](mvc-music-store-part-8/_static/image3.png)

<span data-ttu-id="76547-172">Ancak, sepetten öğeleri kaldırmak için bir HTML. ActionLink kullanmak yerine, bu görünümdeki HTML sınıfı RemoveLink 'e sahip tüm bağlantılar için tıklama olayını "kullanıma almak" amacıyla jQuery kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="76547-172">However, instead of using an Html.ActionLink to remove items from the cart, we'll use jQuery to "wire up" the click event for all links in this view which have the HTML class RemoveLink.</span></span> <span data-ttu-id="76547-173">Formu deftere nakletmek yerine, bu tıklama olayı işleyicisi yalnızca RemoveFromCart Controller eylemmiz için bir AJAX geri araması yapar.</span><span class="sxs-lookup"><span data-stu-id="76547-173">Rather than posting the form, this click event handler will just make an AJAX callback to our RemoveFromCart controller action.</span></span> <span data-ttu-id="76547-174">RemoveFromCart, jQuery geri çağırduğumuz, daha sonra jQuery kullanarak sayfada dört hızlı güncelleştirme gerçekleştiren JSON serileştirilmiş sonucunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="76547-174">The RemoveFromCart returns a JSON serialized result, which our jQuery callback then parses and performs four quick updates to the page using jQuery:</span></span>

- 1. <span data-ttu-id="76547-175">Silinen albümü listeden kaldırır</span><span class="sxs-lookup"><span data-stu-id="76547-175">Removes the deleted album from the list</span></span>
- 2. <span data-ttu-id="76547-176">Başlıktaki sepet sayısını güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="76547-176">Updates the cart count in the header</span></span>
- 3. <span data-ttu-id="76547-177">Kullanıcıya bir güncelleştirme iletisi görüntüler</span><span class="sxs-lookup"><span data-stu-id="76547-177">Displays an update message to the user</span></span>
- 4. <span data-ttu-id="76547-178">Sepet toplam fiyatını güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="76547-178">Updates the cart total price</span></span>

<span data-ttu-id="76547-179">Kaldırma senaryosu dizin görünümü içinde bir AJAX geri çağırması tarafından işlendiğinden, RemoveFromCart Action için ek bir görünüm gerekmez.</span><span class="sxs-lookup"><span data-stu-id="76547-179">Since the remove scenario is being handled by an Ajax callback within the Index view, we don't need an additional view for RemoveFromCart action.</span></span> <span data-ttu-id="76547-180">/ShoppingCart/Index görünümü için kodun tamamı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="76547-180">Here is the complete code for the /ShoppingCart/Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

<span data-ttu-id="76547-181">Bunu test etmek için, alışveriş sepetimize öğe ekleyebilmemiz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="76547-181">In order to test this out, we need to be able to add items to our shopping cart.</span></span> <span data-ttu-id="76547-182">**Mağaza ayrıntıları** görünümümüzü "sepetin Ekle" düğmesi içerecek şekilde güncelleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="76547-182">We'll update our **Store Details** view to include an "Add to cart" button.</span></span> <span data-ttu-id="76547-183">Bu noktada, bu görünümü son güncelleştirdiğimiz zamandan sonra eklediğimiz bazı albüm ek bilgilerini de dahil eteceğiz: tarz, sanatçı, Fiyat ve albüm resmi.</span><span class="sxs-lookup"><span data-stu-id="76547-183">While we're at it, we can include some of the Album additional information which we've added since we last updated this view: Genre, Artist, Price, and Album Art.</span></span> <span data-ttu-id="76547-184">Güncelleştirilmiş mağaza Ayrıntıları görünümü kodu aşağıda gösterildiği gibi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="76547-184">The updated Store Details view code appears as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

<span data-ttu-id="76547-185">Şimdi mağazaya tıklayabilir ve alışveriş sepetimize ve ' ye Albümler ekleme ve kaldırma testi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76547-185">Now we can click through the store and test adding and removing Albums to and from our shopping cart.</span></span> <span data-ttu-id="76547-186">Uygulamayı çalıştırın ve mağaza dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="76547-186">Run the application and browse to the Store Index.</span></span>

![](mvc-music-store-part-8/_static/image4.png)

<span data-ttu-id="76547-187">Ardından, albümler listesini görüntülemek için bir tarz üzerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="76547-187">Next, click on a Genre to view a list of albums.</span></span>

![](mvc-music-store-part-8/_static/image5.png)

<span data-ttu-id="76547-188">Bir albüm başlığına tıkladığınızda, "Sepete Ekle" düğmesi de dahil olmak üzere güncelleştirilmiş Albüm Ayrıntıları görünümü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="76547-188">Clicking on an Album title now shows our updated Album Details view, including the "Add to cart" button.</span></span>

![](mvc-music-store-part-8/_static/image6.png)

<span data-ttu-id="76547-189">"Sepete Ekle" düğmesine tıklamak, alışveriş sepeti özet listesi ile alışveriş sepeti Dizin görünümümüzü gösterir.</span><span class="sxs-lookup"><span data-stu-id="76547-189">Clicking the "Add to cart" button shows our Shopping Cart Index view with the shopping cart summary list.</span></span>

![](mvc-music-store-part-8/_static/image7.png)

<span data-ttu-id="76547-190">Alışveriş sepetinizi yükledikten sonra, alışveriş sepetinize yönelik Ajax güncelleştirmesini görmek için sepeden Kaldır bağlantısına tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76547-190">After loading up your shopping cart, you can click on the Remove from cart link to see the Ajax update to your shopping cart.</span></span>

![](mvc-music-store-part-8/_static/image8.png)

<span data-ttu-id="76547-191">Kayıtsız kullanıcıların sepetlerinde öğe eklemesine izin veren bir çalışan alışveriş sepeti oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="76547-191">We've built out a working shopping cart which allows unregistered users to add items to their cart.</span></span> <span data-ttu-id="76547-192">Aşağıdaki bölümde, kullanıma alma işleminin kaydolmasını ve tamamlanmasına izin vereceğiz.</span><span class="sxs-lookup"><span data-stu-id="76547-192">In the following section, we'll allow them to register and complete the checkout process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="76547-193">[Önceki](mvc-music-store-part-7.md)
> [İleri](mvc-music-store-part-9.md)</span><span class="sxs-lookup"><span data-stu-id="76547-193">[Previous](mvc-music-store-part-7.md)
[Next](mvc-music-store-part-9.md)</span></span>
