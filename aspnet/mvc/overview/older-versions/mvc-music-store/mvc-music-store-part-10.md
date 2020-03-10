---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: '10. kısım: gezinti ve site tasarımına yönelik son güncelleştirmeler, sonuç | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 10, gezinti ve S için son güncelleştirmeleri içerir...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539370"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a><span data-ttu-id="42e5a-104">10. Bölüm: Gezinti ve Site Tasarımına Yönelik Son Güncelleştirmeler, Sonuç</span><span class="sxs-lookup"><span data-stu-id="42e5a-104">Part 10: Final Updates to Navigation and Site Design, Conclusion</span></span>

<span data-ttu-id="42e5a-105">[Jon Galloway](https://github.com/jongalloway) tarafından</span><span class="sxs-lookup"><span data-stu-id="42e5a-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="42e5a-106">MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="42e5a-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="42e5a-107">MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="42e5a-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="42e5a-108">Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="42e5a-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="42e5a-109">Bölüm 10 ' da gezinti ve site tasarımı için son güncelleştirmeler ve sonuç olarak yer alır.</span><span class="sxs-lookup"><span data-stu-id="42e5a-109">Part 10 covers Final Updates to Navigation and Site Design, Conclusion.</span></span>

<span data-ttu-id="42e5a-110">Sitemizin tüm önemli işlevlerini tamamladık, ancak hala site gezintisine, giriş sayfasına ve mağaza tarama sayfasına eklemek için bazı özellikler sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-110">We've completed all the major functionality for our site, but we still have some features to add to the site navigation, the home page, and the Store Browse page.</span></span>

## <a name="creating-the-shopping-cart-summary-partial-view"></a><span data-ttu-id="42e5a-111">Alışveriş sepeti Özeti kısmi görünümü oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="42e5a-111">Creating the Shopping Cart Summary Partial View</span></span>

<span data-ttu-id="42e5a-112">Kullanıcının alışveriş sepetindeki öğe sayısını tüm site genelinde göstermek istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-112">We want to expose the number of items in the user's shopping cart across the entire site.</span></span>

![](mvc-music-store-part-10/_static/image1.png)

<span data-ttu-id="42e5a-113">Bunu, sitemiz. Master ' a eklenen kısmi bir görünüm oluşturarak kolayca uygulayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-113">We can easily implement this by creating a partial view which is added to our Site.master.</span></span>

<span data-ttu-id="42e5a-114">Daha önce gösterildiği gibi, ShoppingCart denetleyicisi kısmi bir görünüm döndüren bir CartSummary eylem yöntemi içerir:</span><span class="sxs-lookup"><span data-stu-id="42e5a-114">As shown previously, the ShoppingCart controller includes a CartSummary action method which returns a partial view:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

<span data-ttu-id="42e5a-115">CartSummary kısmi görünümü oluşturmak için, görünümler/ShoppingCart klasörüne sağ tıklayın ve Görünüm Ekle ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="42e5a-115">To create the CartSummary partial view, right-click on the Views/ShoppingCart folder and select Add View.</span></span> <span data-ttu-id="42e5a-116">Görünümü CartSummary olarak adlandırın ve aşağıda gösterildiği gibi "kısmi görünüm oluştur" onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="42e5a-116">Name the view CartSummary and check the "Create a partial view" checkbox as shown below.</span></span>

![](mvc-music-store-part-10/_static/image2.png)

<span data-ttu-id="42e5a-117">CartSummary kısmi görünümü gerçekten basittir. Bu yalnızca, sepetteki öğelerin sayısını gösteren ShoppingCart dizin görünümüne yönelik bir bağlantıdır.</span><span class="sxs-lookup"><span data-stu-id="42e5a-117">The CartSummary partial view is really simple - it's just a link to the ShoppingCart Index view which shows the number of items in the cart.</span></span> <span data-ttu-id="42e5a-118">CartSummary. cshtml için kodun tamamı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="42e5a-118">The complete code for CartSummary.cshtml is as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

<span data-ttu-id="42e5a-119">Site Yöneticisi de dahil olmak üzere sitedeki herhangi bir sayfaya, HTML. RenderAction yöntemini kullanarak kısmi bir görünüm dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-119">We can include a partial view in any page in the site, including the Site master, by using the Html.RenderAction method.</span></span> <span data-ttu-id="42e5a-120">RenderAction, aşağıdaki gibi eylem adını ("CartSummary") ve denetleyici adını ("ShoppingCart") belirtmemizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="42e5a-120">RenderAction requires us to specify the Action Name ("CartSummary") and the Controller Name ("ShoppingCart") as below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

<span data-ttu-id="42e5a-121">Bunu site düzenine eklemeden önce, tüm site. Master güncelleştirmelerini tek seferde yapabilmemiz için de tarz menüsünü oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="42e5a-121">Before adding this to the site Layout, we will also create the Genre Menu so we can make all of our Site.master updates at one time.</span></span>

## <a name="creating-the-genre-menu-partial-view"></a><span data-ttu-id="42e5a-122">Tarzı menü kısmi görünümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="42e5a-122">Creating the Genre Menu Partial View</span></span>

<span data-ttu-id="42e5a-123">Mağazalarımızda bulunan tüm tarzları listeleyen bir tarz menü ekleyerek kullanıcılarımızın mağazada gezinilmesi çok daha kolay olabilir.</span><span class="sxs-lookup"><span data-stu-id="42e5a-123">We can make it a lot easier for our users to navigate through the store by adding a Genre Menu which lists all the Genres available in our store.</span></span>

![](mvc-music-store-part-10/_static/image3.png)

<span data-ttu-id="42e5a-124">Aynı adımları izleyerek bir GenreMenu kısmi görünümü oluşturur ve bunları hem site yöneticisine ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-124">We will follow the same steps also create a GenreMenu partial view, and then we can add them both to the Site master.</span></span> <span data-ttu-id="42e5a-125">Önce, StoreController öğesine aşağıdaki GenreMenu denetleyici eylemini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="42e5a-125">First, add the following GenreMenu controller action to the StoreController:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

<span data-ttu-id="42e5a-126">Bu eylem, daha sonra oluşturduğumuz kısmi görünüm tarafından görüntülenecek olan tarzın bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="42e5a-126">This action returns a list of Genres which will be displayed by the partial view, which we will create next.</span></span>

<span data-ttu-id="42e5a-127">*Note: Bu denetleyiciye yalnızca bu eylemin yalnızca bir kısmi görünümden kullanılmasını istediğinizi belirten bu denetleyici eylemine [Childadctiononly] özniteliğini ekledik. Bu öznitelik,/Store/genremenu'e göz atarak denetleyici eyleminin yürütülmesini engeller. Bu, kısmi görünümler için gerekli değildir, ancak denetleyici eylemlerimizin amaçladığınız şekilde kullanıldığından emin olmak istediğimiz için iyi bir uygulamadır. Ayrıca, görüntüleme altyapısının diğer görünümlere eklendiğinden Bu görünüm için Düzen kullanması gerektiğini bilmesini sağlayan, görüntüleme yerine PartialView döndürüyoruz.*</span><span class="sxs-lookup"><span data-stu-id="42e5a-127">*Note: We have added the [ChildActionOnly] attribute to this controller action, which indicates that we only want this action to be used from a Partial View. This attribute will prevent the controller action from being executed by browsing to /Store/GenreMenu. This isn't required for partial views, but it is a good practice, since we want to make sure our controller actions are used as we intend. We are also returning PartialView rather than View, which lets the view engine know that it shouldn't use the Layout for this view, as it is being included in other views.*</span></span>

<span data-ttu-id="42e5a-128">GenreMenu denetleyicisi eylemine sağ tıklayın ve aşağıda gösterildiği gibi tarzı görünüm verisi sınıfı kullanılarak kesin bir şekilde belirlenmiş olan GenreMenu adlı kısmi bir görünüm oluşturun.</span><span class="sxs-lookup"><span data-stu-id="42e5a-128">Right-click on the GenreMenu controller action and create a partial view named GenreMenu which is strongly typed using the Genre view data class as shown below.</span></span>

![](mvc-music-store-part-10/_static/image4.png)

<span data-ttu-id="42e5a-129">Aşağıdaki gibi sıralanmamış bir liste kullanarak öğeleri görüntülemek için GenreMenu kısmi görünümünün görünüm kodunu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="42e5a-129">Update the view code for the GenreMenu partial view to display the items using an unordered list as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a><span data-ttu-id="42e5a-130">Kısmi Görünümlerimizi göstermek için site düzeni güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="42e5a-130">Updating Site Layout to display our Partial Views</span></span>

<span data-ttu-id="42e5a-131">HTML. RenderAction () yöntemini çağırarak kısmi Görünümlerimizi site düzenine (/Views/Shared/\_Layout. cshtml) ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-131">We can add our partial views to the Site Layout (/Views/Shared/\_Layout.cshtml) by calling Html.RenderAction().</span></span> <span data-ttu-id="42e5a-132">Bunları, aşağıda gösterildiği gibi, bunlara ek olarak bunları göstermek için de ekleyeceğiz:</span><span class="sxs-lookup"><span data-stu-id="42e5a-132">We'll add them both in, as well as some additional markup to display them, as shown below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

<span data-ttu-id="42e5a-133">Artık uygulamayı çalıştırdığımızda, sol gezinti alanında tarzı ve en üstteki sepet özetini görüyoruz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-133">Now when we run the application, we will see the Genre in the left navigation area and the Cart Summary at the top.</span></span>

## <a name="update-to-the-store-browse-page"></a><span data-ttu-id="42e5a-134">Mağaza tarayıcı sayfasına Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="42e5a-134">Update to the Store Browse page</span></span>

<span data-ttu-id="42e5a-135">Mağaza göz at sayfası işlevseldir, ancak çok iyi görünmüyor.</span><span class="sxs-lookup"><span data-stu-id="42e5a-135">The Store Browse page is functional, but doesn't look very good.</span></span> <span data-ttu-id="42e5a-136">Görünüm kodunu güncelleştirerek (/Views/Store/Browse.cshtml içinde bulunur), daha iyi bir düzende Albümler göstermek için sayfayı güncelleştirebiliriz:</span><span class="sxs-lookup"><span data-stu-id="42e5a-136">We can update the page to show the albums in a better layout by updating the view code (found in /Views/Store/Browse.cshtml) as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

<span data-ttu-id="42e5a-137">Burada, albüm resmini eklemek için bağlantıya özel biçimlendirme uygulayabilmemiz için HTML. ActionLink yerine URL. Action ' i kullanırız.</span><span class="sxs-lookup"><span data-stu-id="42e5a-137">Here we are making use of Url.Action rather than Html.ActionLink so that we can apply special formatting to the link to include the album artwork.</span></span>

<span data-ttu-id="42e5a-138">*Note: Bu Albümler için genel bir albüm kapağı görüntüliyoruz. Bu bilgiler veritabanında depolanır ve mağaza Yöneticisi aracılığıyla düzenlenebilir. Kendi resminizi eklemek için hoş geldiniz.*</span><span class="sxs-lookup"><span data-stu-id="42e5a-138">*Note: We are displaying a generic album cover for these albums. This information is stored in the database and is editable via the Store Manager. You are welcome to add your own artwork.*</span></span>

<span data-ttu-id="42e5a-139">Şimdi bir Tarzya gözatarken, albüm resmindeki bir kılavuzda gösterilen albümleri görüyoruz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-139">Now when we browse to a Genre, we will see the albums shown in a grid with the album artwork.</span></span>

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a><span data-ttu-id="42e5a-140">Ana sayfayı, En Iyi satış albümlerini gösterecek şekilde güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="42e5a-140">Updating the Home Page to show Top Selling Albums</span></span>

<span data-ttu-id="42e5a-141">Satışları artırmak için ana sayfada en iyi satış albümlerimizi kullanmak istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-141">We want to feature our top selling albums on the home page to increase sales.</span></span> <span data-ttu-id="42e5a-142">Bu bilgileri işlemek için HomeController 'da bazı güncelleştirmeler oluşturacağız ve bazı ek grafikler de ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-142">We'll make some updates to our HomeController to handle that, and add in some additional graphics as well.</span></span>

<span data-ttu-id="42e5a-143">İlk olarak, EntityFramework 'ün ilişkilendirildikleri bilmesini sağlamak için, albüm sınıfmıza bir gezinti özelliği ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-143">First, we'll add a navigation property to our Album class so that EntityFramework knows that they're associated.</span></span> <span data-ttu-id="42e5a-144">**Albüm** sınıfınızın son birkaç satırı şu şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="42e5a-144">The last few lines of our **Album** class should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

<span data-ttu-id="42e5a-145">*Note: Bu, System. Collections. Generic ad alanını getirmek için using ifadesinin eklenmesini gerektirir.*</span><span class="sxs-lookup"><span data-stu-id="42e5a-145">*Note: This will require adding a using statement to bring in the System.Collections.Generic namespace.*</span></span>

<span data-ttu-id="42e5a-146">İlk olarak, diğer denetleyicilerimizde olduğu gibi deyimlerini kullanarak bir storeDB alanı ve MvcMusicStore. modeller ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-146">First, we'll add a storeDB field and the MvcMusicStore.Models using statements, as in our other controllers.</span></span> <span data-ttu-id="42e5a-147">Daha sonra, OrderDetails 'e göre en popüler satış albümleri bulmak için veritabanımızı sorgulayan HomeController öğesine aşağıdaki yöntemi ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-147">Next, we'll add the following method to the HomeController which queries our database to find top selling albums according to OrderDetails.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

<span data-ttu-id="42e5a-148">Bu, bir denetleyici eylemi olarak kullanılabilir hale getirmek istemediğimiz için özel bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="42e5a-148">This is a private method, since we don't want to make it available as a controller action.</span></span> <span data-ttu-id="42e5a-149">Bunu basitlik için HomeController içine dahil ediyoruz, ancak iş mantığınızı uygun şekilde ayrı hizmet sınıflarına taşımanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="42e5a-149">We are including it in the HomeController for simplicity, but you are encouraged to move your business logic into separate service classes as appropriate.</span></span>

<span data-ttu-id="42e5a-150">Bu şekilde, Dizin denetleyicisi eylemini en iyi 5 satış albümlerini sorgulamak ve görünüme döndürmek için güncelleştirebiliriz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-150">With that in place, we can update the Index controller action to query the top 5 selling albums and return them to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

<span data-ttu-id="42e5a-151">Güncelleştirilmiş HomeController için kodun tamamı aşağıda gösterildiği gibidir.</span><span class="sxs-lookup"><span data-stu-id="42e5a-151">The complete code for the updated HomeController is as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

<span data-ttu-id="42e5a-152">Son olarak, model türünü güncelleştirerek ve albüm listesini Alta ekleyerek bir albüm listesi görüntülemesi için giriş dizini görünümümüzü güncelleştirmemiz gerekir.</span><span class="sxs-lookup"><span data-stu-id="42e5a-152">Finally, we'll need to update our Home Index view so that it can display a list of albums by updating the Model type and adding the album list to the bottom.</span></span> <span data-ttu-id="42e5a-153">Ayrıca, sayfaya bir başlık ve promosyon bölümü de eklemek için bu fırsatı ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="42e5a-153">We will take this opportunity to also add a heading and a promotion section to the page.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

<span data-ttu-id="42e5a-154">Artık uygulamayı çalıştırdığımızda, en çok satılan albümler ve tanıtım mesajımız ile güncelleştirilmiş giriş sayfamızı görüyoruz.</span><span class="sxs-lookup"><span data-stu-id="42e5a-154">Now when we run the application, we'll see our updated home page with top selling albums and our promotional message.</span></span>

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a><span data-ttu-id="42e5a-155">Sonuç</span><span class="sxs-lookup"><span data-stu-id="42e5a-155">Conclusion</span></span>

<span data-ttu-id="42e5a-156">ASP.NET MVC 'nin veritabanı erişimi, üyeliği, AJAX vb. ile gelişmiş bir Web sitesi oluşturmayı kolaylaştırdığını gördük.</span><span class="sxs-lookup"><span data-stu-id="42e5a-156">We've seen that ASP.NET MVC makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="42e5a-157">oldukça hızlı.</span><span class="sxs-lookup"><span data-stu-id="42e5a-157">pretty quickly.</span></span> <span data-ttu-id="42e5a-158">Bu öğreticide, kendi ASP.NET MVC uygulamalarınızı oluşturmaya başlamak için ihtiyacınız olan araçları vermiş olursunuz!</span><span class="sxs-lookup"><span data-stu-id="42e5a-158">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET MVC applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="42e5a-159">Öncekini</span><span class="sxs-lookup"><span data-stu-id="42e5a-159">Previous</span></span>](mvc-music-store-part-9.md)
