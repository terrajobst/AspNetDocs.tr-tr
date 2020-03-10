---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: '9\. Bölüm: kayıt ve kullanıma alma | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 9 ' da kayıt ve kullanıma alma ele alınmaktadır.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559537"
---
# <a name="part-9-registration-and-checkout"></a><span data-ttu-id="ca3ee-104">9\. Bölüm: Kayıt ve Kasa İşlemleri</span><span class="sxs-lookup"><span data-stu-id="ca3ee-104">Part 9: Registration and Checkout</span></span>

<span data-ttu-id="ca3ee-105">[Jon Galloway](https://github.com/jongalloway) tarafından</span><span class="sxs-lookup"><span data-stu-id="ca3ee-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="ca3ee-106">MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="ca3ee-107">MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="ca3ee-108">Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="ca3ee-109">Bölüm 9 ' da kayıt ve kullanıma alma ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-109">Part 9 covers Registration and Checkout.</span></span>

<span data-ttu-id="ca3ee-110">Bu bölümde, alışverişçinin adresini ve ödeme bilgilerini toplayacak bir CheckoutController oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-110">In this section, we will be creating a CheckoutController which will collect the shopper's address and payment information.</span></span> <span data-ttu-id="ca3ee-111">Kullanıcıların kullanıma almadan önce sitemizi kaydetmesi gerekir, bu nedenle bu denetleyici yetkilendirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-111">We will require users to register with our site prior to checking out, so this controller will require authorization.</span></span>

<span data-ttu-id="ca3ee-112">Kullanıcılar, "kullanıma al" düğmesine tıklayarak alışveriş sepetinden kullanıma alma işlemine gidecektir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-112">Users will navigate to the checkout process from their shopping cart by clicking the "Checkout" button.</span></span>

![](mvc-music-store-part-9/_static/image1.jpg)

<span data-ttu-id="ca3ee-113">Kullanıcı oturum açmadıysa, bu kullanıcılara sorulur.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-113">If the user is not logged in, they will be prompted to.</span></span>

![](mvc-music-store-part-9/_static/image1.png)

<span data-ttu-id="ca3ee-114">Oturum başarıyla tamamlandığında, Kullanıcı Adres ve ödeme görünümü gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-114">Upon successful login, the user is then shown the Address and Payment view.</span></span>

![](mvc-music-store-part-9/_static/image2.png)

<span data-ttu-id="ca3ee-115">Formu doldurduktan ve siparişi gönderdikten sonra, bu sipariş onay ekranı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-115">Once they have filled the form and submitted the order, they will be shown the order confirmation screen.</span></span>

![](mvc-music-store-part-9/_static/image3.png)

<span data-ttu-id="ca3ee-116">Varolmayan bir siparişi veya size ait olmayan bir siparişi görüntüleme girişimi hata görünümünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-116">Attempting to view either a non-existent order or an order that doesn't belong to you will show the Error view.</span></span>

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="ca3ee-117">Alışveriş sepetini geçirme</span><span class="sxs-lookup"><span data-stu-id="ca3ee-117">Migrating the Shopping Cart</span></span>

<span data-ttu-id="ca3ee-118">Alışveriş süreci anonim olsa da, Kullanıcı kullanıma al düğmesine tıkladığında, kaydolmaları ve oturum açması gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-118">While the shopping process is anonymous, when the user clicks on the Checkout button, they will be required to register and login.</span></span> <span data-ttu-id="ca3ee-119">Kullanıcılar, alışveriş sepeti bilgilerini ziyaret ettikleri sırada koruduğumuz için, kayıt veya oturum açma bilgilerini tamamladıktan sonra alışveriş sepeti bilgilerini bir kullanıcıyla ilişkilendirmemiz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-119">Users will expect that we will maintain their shopping cart information between visits, so we will need to associate the shopping cart information with a user when they complete registration or login.</span></span>

<span data-ttu-id="ca3ee-120">Bu aslında çok basittir çünkü, ShoppingCart sınıfınız zaten geçerli sepetteki tüm öğeleri bir kullanıcı adıyla ilişkilendirecek bir yönteme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-120">This is actually very simple to do, as our ShoppingCart class already has a method which will associate all the items in the current cart with a username.</span></span> <span data-ttu-id="ca3ee-121">Bir kullanıcı kayıt veya oturum açma işlemini tamamlarsa bu yöntemi çağıracağız.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-121">We will just need to call this method when a user completes registration or login.</span></span>

<span data-ttu-id="ca3ee-122">Üyelik ve yetkilendirme ayarlamamız sırasında eklediğimiz **accountcontroller** sınıfını açın.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-122">Open the **AccountController** class that we added when we were setting up Membership and Authorization.</span></span> <span data-ttu-id="ca3ee-123">MvcMusicStore. modellerine başvuran bir using açıklaması ekleyin ve ardından aşağıdaki MigrateShoppingCart metodunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ca3ee-123">Add a using statement referencing MvcMusicStore.Models, then add the following MigrateShoppingCart method:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

<span data-ttu-id="ca3ee-124">Sonra, aşağıda gösterildiği gibi, Kullanıcı doğrulandıktan sonra MigrateShoppingCart ' ı çağırmak için oturum açma sonrası eylemini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ca3ee-124">Next, modify the LogOn post action to call MigrateShoppingCart after the user has been validated, as shown below:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

<span data-ttu-id="ca3ee-125">Kullanıcı hesabı başarıyla oluşturulduktan hemen sonra, kaydı kaydet eyleminde aynı değişikliği yapın:</span><span class="sxs-lookup"><span data-stu-id="ca3ee-125">Make the same change to the Register post action, immediately after the user account is successfully created:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

<span data-ttu-id="ca3ee-126">Bu, artık başarılı kayıt veya oturum açma işlemi sırasında anonim bir alışveriş sepeti otomatik olarak bir kullanıcı hesabına aktarılır.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-126">That's it - now an anonymous shopping cart will be automatically transferred to a user account upon successful registration or login.</span></span>

## <a name="creating-the-checkoutcontroller"></a><span data-ttu-id="ca3ee-127">CheckoutController oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca3ee-127">Creating the CheckoutController</span></span>

<span data-ttu-id="ca3ee-128">Denetleyiciler klasörüne sağ tıklayın ve boş denetleyici şablonunu kullanarak CheckoutController adlı projeye yeni bir denetleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-128">Right-click on the Controllers folder and add a new Controller to the project named CheckoutController using the Empty controller template.</span></span>

![](mvc-music-store-part-9/_static/image5.png)

<span data-ttu-id="ca3ee-129">İlk olarak, kullanıcıların kullanıma almadan önce kaydolmayı gerektirmek için denetleyici sınıfı bildiriminin üzerine Yetkilendir özniteliğini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ca3ee-129">First, add the Authorize attribute above the Controller class declaration to require users to register before checkout:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

<span data-ttu-id="ca3ee-130">*Note: Bu, daha önce StoreManagerController 'a yaptığımız değişikliğe benzerdir, ancak bu durumda Yetkilendir özniteliği kullanıcının yönetici rolünde olması gerekir. Kullanıma alma denetleyicisinde, kullanıcının oturum açmasını ve yöneticiler olmasını gerektirmeyi istiyoruz.*</span><span class="sxs-lookup"><span data-stu-id="ca3ee-130">*Note: This is similar to the change we previously made to the StoreManagerController, but in that case the Authorize attribute required that the user be in an Administrator role. In the Checkout Controller, we're requiring the user be logged in but aren't requiring that they be administrators.*</span></span>

<span data-ttu-id="ca3ee-131">Kolaylık sağlaması için bu öğreticide ödeme bilgileriyle ilgilenmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-131">For the sake of simplicity, we won't be dealing with payment information in this tutorial.</span></span> <span data-ttu-id="ca3ee-132">Bunun yerine, kullanıcıların tanıtım kodu kullanarak kullanıma almalarına izin veririz.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-132">Instead, we are allowing users to check out using a promotional code.</span></span> <span data-ttu-id="ca3ee-133">Bu promosyon kodunu PromoCode adlı bir sabit kullanarak depolayacağız.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-133">We will store this promotional code using a constant named PromoCode.</span></span>

<span data-ttu-id="ca3ee-134">StoreController 'da olduğu gibi, storeDB adlı MusicStoreEntities sınıfının bir örneğini tutmak için bir alan tanımlayacağız.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-134">As in the StoreController, we'll declare a field to hold an instance of the MusicStoreEntities class, named storeDB.</span></span> <span data-ttu-id="ca3ee-135">MusicStoreEntities sınıfını kullanabilmeniz için, MvcMusicStore. model ad alanı için bir using ifadesini eklememiz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-135">In order to make use of the MusicStoreEntities class, we will need to add a using statement for the MvcMusicStore.Models namespace.</span></span> <span data-ttu-id="ca3ee-136">Kullanıma alma denetleyicimizin en üstü aşağıda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-136">The top of our Checkout controller appears below.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

<span data-ttu-id="ca3ee-137">CheckoutController aşağıdaki denetleyici eylemlerine sahip olacaktır:</span><span class="sxs-lookup"><span data-stu-id="ca3ee-137">The CheckoutController will have the following controller actions:</span></span>

<span data-ttu-id="ca3ee-138">**Addressandödemeler (get yöntemi)** , kullanıcının bilgilerini girmesine izin veren bir form görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-138">**AddressAndPayment (GET method)** will display a form to allow the user to enter their information.</span></span>

<span data-ttu-id="ca3ee-139">**Addressandödemeler (POST yöntemi)** girişi doğrular ve siparişi işler.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-139">**AddressAndPayment (POST method)** will validate the input and process the order.</span></span>

<span data-ttu-id="ca3ee-140">Bir Kullanıcı, kullanıma alma işlemini başarıyla tamamladıktan sonra, **tamamlandı** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-140">**Complete** will be shown after a user has successfully finished the checkout process.</span></span> <span data-ttu-id="ca3ee-141">Bu görünüm kullanıcının sıra numarasını onay olarak içerecektir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-141">This view will include the user's order number, as confirmation.</span></span>

<span data-ttu-id="ca3ee-142">İlk olarak, Dizin denetleyicisi eylemini (denetleyiciyi oluşturduğumuz sırada oluşturulmuştur) adreslemek için yeniden adlandıralım.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-142">First, let's rename the Index controller action (which was generated when we created the controller) to AddressAndPayment.</span></span> <span data-ttu-id="ca3ee-143">Bu denetleyici eylemi yalnızca kullanıma alma formunu görüntüler, bu nedenle herhangi bir model bilgisi gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-143">This controller action just displays the checkout form, so it doesn't require any model information.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

<span data-ttu-id="ca3ee-144">Addressandödeme POST yöntemi, StoreManagerController 'da kullandığımız aynı düzeni izlemelidir: form gönderimini kabul edip sırayı tamamlamaya çalışır ve başarısız olursa formu yeniden görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-144">Our AddressAndPayment POST method will follow the same pattern we used in the StoreManagerController: it will try to accept the form submission and complete the order, and will re-display the form if it fails.</span></span>

<span data-ttu-id="ca3ee-145">Form girişi doğrulandıktan sonra bir sipariş için doğrulama gereksinimlerimizi karşılıyorsa, PromoCode form değerini doğrudan denetleriz.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-145">After validating the form input meets our validation requirements for an Order, we will check the PromoCode form value directly.</span></span> <span data-ttu-id="ca3ee-146">Her şeyin doğru olduğu varsayıldığında, güncelleştirilmiş bilgileri sırasıyla kaydedecek, ShoppingCart nesnesine sipariş sürecini tamamlayacak ve tamamlanmış eyleme yönlendireceğiz.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-146">Assuming everything is correct, we will save the updated information with the order, tell the ShoppingCart object to complete the order process, and redirect to the Complete action.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

<span data-ttu-id="ca3ee-147">Kullanıma alma işleminin başarıyla tamamlanmasından sonra, kullanıcılar tüm denetleyiciye yeniden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-147">Upon successful completion of the checkout process, users will be redirected to the Complete controller action.</span></span> <span data-ttu-id="ca3ee-148">Bu eylem, sipariş numarasını onay olarak göstermeden önce siparişin, oturum açmış kullanıcıya ait olduğunu doğrulamak için basit bir denetim gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-148">This action will perform a simple check to validate that the order does indeed belong to the logged-in user before showing the order number as a confirmation.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

<span data-ttu-id="ca3ee-149">*Note: projeyi başladığımızda, hata görünümü/Views/Shared klasöründe bizim için otomatik olarak oluşturuldu.*</span><span class="sxs-lookup"><span data-stu-id="ca3ee-149">*Note: The Error view was automatically created for us in the /Views/Shared folder when we began the project.*</span></span>

<span data-ttu-id="ca3ee-150">Tüm CheckoutController kodu aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ca3ee-150">The complete CheckoutController code is as follows:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a><span data-ttu-id="ca3ee-151">Addressandödeme görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="ca3ee-151">Adding the AddressAndPayment view</span></span>

<span data-ttu-id="ca3ee-152">Şimdi Addressandödeme görünümünü oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-152">Now, let's create the AddressAndPayment view.</span></span> <span data-ttu-id="ca3ee-153">Addressandödeme denetleyicisi eylemlerinden birine sağ tıklayın ve bir sipariş olarak kesin olarak belirlenmiş olan Addressandödeme adlı bir görünüm ekleyin ve aşağıda gösterildiği gibi düzenleme şablonunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-153">Right-click on one of the AddressAndPayment controller actions and add a view named AddressAndPayment which is strongly typed as an Order and uses the Edit template, as shown below.</span></span>

![](mvc-music-store-part-9/_static/image6.png)

<span data-ttu-id="ca3ee-154">Bu görünüm StoreManagerEdit görünümünü oluştururken bakdığımız tekniklerin ikisini de kullanacaktır:</span><span class="sxs-lookup"><span data-stu-id="ca3ee-154">This view will make use of two of the techniques we looked at while building the StoreManagerEdit view:</span></span>

- <span data-ttu-id="ca3ee-155">Sipariş modelinin form alanlarını göstermek için HTML. EditorForModel () kullanacağız</span><span class="sxs-lookup"><span data-stu-id="ca3ee-155">We will use Html.EditorForModel() to display form fields for the Order model</span></span>
- <span data-ttu-id="ca3ee-156">Doğrulama öznitelikleriyle bir order Class kullanarak doğrulama kurallarından yararlanacağız</span><span class="sxs-lookup"><span data-stu-id="ca3ee-156">We will leverage validation rules using an Order class with validation attributes</span></span>

<span data-ttu-id="ca3ee-157">Form kodunu, daha sonra promosyon kodu için ek bir TextBox ile HTML. EditorForModel () kullanmak üzere güncelleyerek başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-157">We'll start by updating the form code to use Html.EditorForModel(), followed by an additional textbox for the Promo Code.</span></span> <span data-ttu-id="ca3ee-158">Addressandödeme görünümü için kodun tamamı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-158">The complete code for the AddressAndPayment view is shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a><span data-ttu-id="ca3ee-159">Sıra için doğrulama kuralları tanımlama</span><span class="sxs-lookup"><span data-stu-id="ca3ee-159">Defining validation rules for the Order</span></span>

<span data-ttu-id="ca3ee-160">Görünümümüzün ayarlanmış olduğuna göre, daha önce albüm modeliyle yaptığımız için, sipariş modelimiz için doğrulama kurallarını ayarlayacağız.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-160">Now that our view is set up, we will set up the validation rules for our Order model as we did previously for the Album model.</span></span> <span data-ttu-id="ca3ee-161">Modeller klasörüne sağ tıklayın ve Order adlı bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-161">Right-click on the Models folder and add a class named Order.</span></span> <span data-ttu-id="ca3ee-162">Daha önce albüm için kullandığımız doğrulama özniteliklerine ek olarak, kullanıcının e-posta adresini doğrulamak için de normal bir Ifade kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-162">In addition to the validation attributes we used previously for the Album, we will also be using a Regular Expression to validate the user's email address.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

<span data-ttu-id="ca3ee-163">Form eksik veya geçersiz bilgilerle gönderilmeye çalışıldığında artık istemci tarafı doğrulaması kullanılarak hata iletisi gösterilecektir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-163">Attempting to submit the form with missing or invalid information will now show error message using client-side validation.</span></span>

![](mvc-music-store-part-9/_static/image7.png)

<span data-ttu-id="ca3ee-164">Son olarak, kullanıma alma işlemi için çok fazla iş yaptık. yalnızca birkaç gürültü vardır ve sona erer.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-164">Okay, we've done most of the hard work for the checkout process; we just have a few odds and ends to finish.</span></span> <span data-ttu-id="ca3ee-165">İki basit görünüm eklememiz gerekir ve oturum açma işlemi sırasında sepet bilgilerinin iletileden kaynaklanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-165">We need to add two simple views, and we need to take care of the handoff of the cart information during the login process.</span></span>

## <a name="adding-the-checkout-complete-view"></a><span data-ttu-id="ca3ee-166">Kullanıma alma tamamlanma görünümü ekleniyor</span><span class="sxs-lookup"><span data-stu-id="ca3ee-166">Adding the Checkout Complete view</span></span>

<span data-ttu-id="ca3ee-167">Yalnızca sipariş KIMLIĞINI görüntülemesi gerektiğinden, kullanıma alma tam görünümü oldukça basittir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-167">The Checkout Complete view is pretty simple, as it just needs to display the Order ID.</span></span> <span data-ttu-id="ca3ee-168">Tüm denetleyiciyi sağ tıklatın ve tam olarak bir int olarak yazılmış olan adlı bir görünüm ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-168">Right-click on the Complete controller action and add a view named Complete which is strongly typed as an int.</span></span>

![](mvc-music-store-part-9/_static/image8.png)

<span data-ttu-id="ca3ee-169">Şimdi, aşağıda gösterildiği gibi, sipariş KIMLIĞINI görüntülemek için görünüm kodunu güncelleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-169">Now we will update the view code to display the Order ID, as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a><span data-ttu-id="ca3ee-170">Hata görünümü güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="ca3ee-170">Updating The Error view</span></span>

<span data-ttu-id="ca3ee-171">Varsayılan şablon paylaşılan görünümler klasöründe bir hata görünümü içerir, böylece sitede başka bir yerde yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-171">The default template includes an Error view in the Shared views folder so that it can be re-used elsewhere in the site.</span></span> <span data-ttu-id="ca3ee-172">Bu hata görünümü çok basit bir hata içeriyor ve site düzenimizi kullanmıyor, bu nedenle güncelleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-172">This Error view contains a very simple error and doesn't use our site Layout, so we'll update it.</span></span>

<span data-ttu-id="ca3ee-173">Bu genel bir hata sayfası olduğundan, içerik çok basittir.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-173">Since this is a generic error page, the content is very simple.</span></span> <span data-ttu-id="ca3ee-174">Kullanıcı eylemini yeniden denemek isterse, geçmişteki bir önceki sayfaya gitmek için bir ileti ve bir bağlantı ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="ca3ee-174">We'll include a message and a link to navigate to the previous page in history if the user wants to re-try their action.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> <span data-ttu-id="ca3ee-175">[Önceki](mvc-music-store-part-8.md)
> [İleri](mvc-music-store-part-10.md)</span><span class="sxs-lookup"><span data-stu-id="ca3ee-175">[Previous](mvc-music-store-part-8.md)
[Next](mvc-music-store-part-10.md)</span></span>
