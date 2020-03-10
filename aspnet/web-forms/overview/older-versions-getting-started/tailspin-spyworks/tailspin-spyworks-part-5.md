---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: '5\. Bölüm: Iş mantığı | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 5\. bölüm bazı iş mantığını ekler.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630307"
---
# <a name="part-5-business-logic"></a><span data-ttu-id="848e6-104">5\. Bölüm: İş Mantığı</span><span class="sxs-lookup"><span data-stu-id="848e6-104">Part 5: Business Logic</span></span>

<span data-ttu-id="848e6-105">[ali Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="848e6-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="848e6-106">Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="848e6-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="848e6-107">Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="848e6-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="848e6-108">Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="848e6-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="848e6-109">5\. bölüm bazı iş mantığını ekler.</span><span class="sxs-lookup"><span data-stu-id="848e6-109">Part 5 adds some business logic.</span></span>

## <a id="_Toc260221671"></a><span data-ttu-id="848e6-110">Iş mantığı ekleme</span><span class="sxs-lookup"><span data-stu-id="848e6-110">Adding Some Business Logic</span></span>

<span data-ttu-id="848e6-111">Her biri web sitemizi ziyaret ettiğinde alışveriş deneyimimizin kullanılabilir olmasını istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="848e6-111">We want our shopping experience to be available whenever someone visits our web site.</span></span> <span data-ttu-id="848e6-112">Ziyaretçiler, kayıtlı veya oturum açmış olmasalar bile alışveriş sepetini ziyaret edebilir ve bunlara öğe ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="848e6-112">Visitors will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="848e6-113">Kullanıma hazır olduklarında, kimlik doğrulama seçeneği verilir ve henüz üye değilse, hesap oluşturabileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="848e6-113">When they are ready to check out they will be given the option to authenticate and if they are not yet members they will be able to create an account.</span></span>

<span data-ttu-id="848e6-114">Bu, alışveriş sepetini anonim bir durumdan "kayıtlı Kullanıcı" durumuna dönüştürmek için mantığı uygulamamız gereken anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="848e6-114">This means that we will need to implement the logic to convert the shopping cart from an anonymous state to a "Registered User" state.</span></span>

<span data-ttu-id="848e6-115">"Classes" adlı bir dizin oluşturalım ve sonra klasöre sağ tıklayıp MyShoppingCart.cs adlı yeni bir "sınıf" dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="848e6-115">Let's create a directory named "Classes" then Right-Click on the folder and create a new "Class" file named MyShoppingCart.cs</span></span>

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

<span data-ttu-id="848e6-116">Daha önce belirtildiği gibi, MyShoppingCart. aspx sayfasını uygulayan sınıfı genişletireceğiz ve bunu kullanarak yapacağız. NET ' in güçlü "kısmi sınıf" yapısı.</span><span class="sxs-lookup"><span data-stu-id="848e6-116">As previously mentioned we will be extending the class that implements the MyShoppingCart.aspx page and we will do this using .NET's powerful "Partial Class" construct.</span></span>

<span data-ttu-id="848e6-117">MyShoppingCart.aspx.cf dosyası için oluşturulan çağrı şuna benzer.</span><span class="sxs-lookup"><span data-stu-id="848e6-117">The generated call for our MyShoppingCart.aspx.cf file looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

<span data-ttu-id="848e6-118">"Partial" anahtar sözcüğünün kullanımını aklınızda edin.</span><span class="sxs-lookup"><span data-stu-id="848e6-118">Note the use of the "partial" keyword.</span></span>

<span data-ttu-id="848e6-119">Yeni oluşturduğumuz sınıf dosyası şuna benzer.</span><span class="sxs-lookup"><span data-stu-id="848e6-119">The class file that we just generated looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

<span data-ttu-id="848e6-120">Bu dosyaya kısmi anahtar sözcük ekleyerek uygulamalarımızı birleştiriyoruz.</span><span class="sxs-lookup"><span data-stu-id="848e6-120">We will merge our implementations by adding the partial keyword to this file as well.</span></span>

<span data-ttu-id="848e6-121">Yeni sınıf dosyanız artık şuna benzer.</span><span class="sxs-lookup"><span data-stu-id="848e6-121">Our new class file now looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

<span data-ttu-id="848e6-122">Sınıfmıza ekleyeceğiniz ilk yöntem "Addidıtem" yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="848e6-122">The first method that we will add to our class is the "AddItem" method.</span></span> <span data-ttu-id="848e6-123">Bu, Kullanıcı ürün listesi ve ürün ayrıntıları sayfalarındaki "resimlere Ekle" bağlantılarına tıkladığında sonunda çağrılacaktır.</span><span class="sxs-lookup"><span data-stu-id="848e6-123">This is the method that will ultimately be called when the user clicks on the "Add to Art" links on the Product List and Product Details pages.</span></span>

<span data-ttu-id="848e6-124">Aşağıdaki, sayfanın en üstündeki using deyimlerine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="848e6-124">Append the following to the using statements at the top of the page.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

<span data-ttu-id="848e6-125">Ve bu yöntemi MyShoppingCart sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="848e6-125">And add this method to the MyShoppingCart class.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

<span data-ttu-id="848e6-126">Öğenin zaten sepette olup olmadığını görmek için LINQ to Entities kullandık.</span><span class="sxs-lookup"><span data-stu-id="848e6-126">We are using LINQ to Entities to see if the item is already in the cart.</span></span> <span data-ttu-id="848e6-127">Bu durumda, öğenin sipariş miktarını güncelleştiririz, aksi takdirde seçili öğe için yeni bir giriş oluşturuyoruz</span><span class="sxs-lookup"><span data-stu-id="848e6-127">If so, we update the order quantity of the item, otherwise we create a new entry for the selected item</span></span>

<span data-ttu-id="848e6-128">Bu yöntemi çağırmak için, yalnızca bu yöntemi sınıftan olmayan bir AddToCart. aspx sayfası uygulayacağız, sonra da öğe eklendikten sonra geçerli alışverişe bir = sepet görüntülendi.</span><span class="sxs-lookup"><span data-stu-id="848e6-128">In order to call this method we will implement an AddToCart.aspx page that not only class this method but then displayed the current shopping a=cart after the item has been added.</span></span>

<span data-ttu-id="848e6-129">Çözüm Gezgini ' nde çözüm adına sağ tıklayın ve daha önce yaptığımız gibi AddToCart. aspx adlı yeni bir sayfa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="848e6-129">Right-Click on the solution name in the solution explorer and add and new page named AddToCart.aspx as we have done previously.</span></span>

<span data-ttu-id="848e6-130">Bu sayfayı, düşük stok sorunları gibi ara sonuçları görüntülemek için kullanabiliriz, ancak uygulamamızda, sayfa aslında işlenmeyecektir, ancak "Ekle" mantığını ve yeniden yönlendirmeyi çağırır.</span><span class="sxs-lookup"><span data-stu-id="848e6-130">While we could use this page to display interim results like low stock issues, etc, in our implementation, the page will not actually render, but rather call the "Add" logic and redirect.</span></span>

<span data-ttu-id="848e6-131">Bunu gerçekleştirmek için, sayfa\_Load olayına aşağıdaki kodu ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="848e6-131">To accomplish this we'll add the following code to the Page\_Load event.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

<span data-ttu-id="848e6-132">Bir QueryString parametresinden alışveriş sepetine eklemek ve sınıfınızın AddItem yöntemini çağırmak için ürünü aldığımızdan emin olmanız gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="848e6-132">Note that we are retrieving the product to add to the shopping cart from a QueryString parameter and calling the AddItem method of our class.</span></span>

<span data-ttu-id="848e6-133">Bir hata ile karşılaşılmayan bir şekilde, bir sonraki adımda uygulayacağız olan SHoppingCart. aspx sayfasına geçirilen hiçbir hatayla karşılaşıyoruz.</span><span class="sxs-lookup"><span data-stu-id="848e6-133">Assuming no errors are encountered control is passed to the SHoppingCart.aspx page which we will fully implement next.</span></span> <span data-ttu-id="848e6-134">Bir hata olması halinde bir özel durum oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="848e6-134">If there should be an error we throw an exception.</span></span>

<span data-ttu-id="848e6-135">Şu anda genel bir hata işleyicisini uyguladık, bu özel durum uygulamamız tarafından işlenmemiş olacak ancak kısa süre içinde devam edeceğiz.</span><span class="sxs-lookup"><span data-stu-id="848e6-135">Currently we have not yet implemented a global error handler so this exception would go unhandled by our application but we will remedy this shortly.</span></span>

<span data-ttu-id="848e6-136">Ayrıca, hata ayıklama. Fail () ifadesinin kullanımı (`using System.Diagnostics;)` aracılığıyla kullanılabilir)</span><span class="sxs-lookup"><span data-stu-id="848e6-136">Note also the use of the statement Debug.Fail() (available via `using System.Diagnostics;)`</span></span>

<span data-ttu-id="848e6-137">Uygulamanın hata ayıklayıcı içinde çalışıyor olması, bu yöntemin, uygulama durumu hakkında bilgiler içeren ayrıntılı bir iletişim kutusu görüntüler ve bu durum, belirlediğimiz hata iletisiyle birlikte, uygulamalar durumu hakkında bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="848e6-137">Is the application is running inside the debugger, this method will display a detailed dialog with information about the applications state along with the error message that we specify.</span></span>

<span data-ttu-id="848e6-138">Üretimde çalışırken Debug. Fail () bildirisi yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="848e6-138">When running in production the Debug.Fail() statement is ignored.</span></span>

<span data-ttu-id="848e6-139">"Getshoppingcartıd" alışveriş sepeti sınıfımızda bir yönteme yapılan çağrının üzerine bir çağrı yukarıdaki kodu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="848e6-139">You will note in the code above a call to a method in our shopping cart class names "GetShoppingCartId".</span></span>

<span data-ttu-id="848e6-140">Yöntemi aşağıdaki şekilde uygulamak için kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="848e6-140">Add the code to implement the method as follows.</span></span>

<span data-ttu-id="848e6-141">Ayrıca, "Toplam" sepetini görüntüleyebilmemiz için güncelleştirme ve kullanıma alma düğmelerini ve bir etiketi ekledik.</span><span class="sxs-lookup"><span data-stu-id="848e6-141">Note that we've also added update and checkout buttons and a label where we can display the cart "total".</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

<span data-ttu-id="848e6-142">Şimdi alışveriş sepetimize öğe ekleyebiliriz, ancak bir ürün eklendikten sonra sepeti görüntüleme mantığını uygulamadık.</span><span class="sxs-lookup"><span data-stu-id="848e6-142">We can now add items to our shopping cart but we have not implemented the logic to display the cart after a product has been added.</span></span>

<span data-ttu-id="848e6-143">Bu nedenle, MyShoppingCart. aspx sayfasında, aşağıdaki gibi bir EntityDataSource denetimi ve GridVire denetimi ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="848e6-143">So, in the MyShoppingCart.aspx page we'll add an EntityDataSource control and a GridVire control as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

<span data-ttu-id="848e6-144">Tasarımcı 'yı Güncelleştir düğmesine çift tıklayarak ve İşaretlemede bildirimde belirtilen Click olay işleyicisini oluşturabilmeniz için formu tasarımcıda çağırın.</span><span class="sxs-lookup"><span data-stu-id="848e6-144">Call up the form in the designer so that you can double click on the Update Cart button and generate the click event handler that is specified in the declaration in the markup.</span></span>

<span data-ttu-id="848e6-145">Ayrıntıları daha sonra uygulayacağız, ancak bunu yaptığınızda uygulamamızı hatasız olarak derleyip çalıştıralım.</span><span class="sxs-lookup"><span data-stu-id="848e6-145">We'll implement the details later but doing this will let us build and run our application without errors.</span></span>

<span data-ttu-id="848e6-146">Uygulamayı çalıştırıp alışveriş sepetine bir öğe eklediğinizde bunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="848e6-146">When you run the application and add an item to the shopping cart you will see this.</span></span>

![](tailspin-spyworks-part-5/_static/image2.jpg)

<span data-ttu-id="848e6-147">Üç özel sütun uygulayarak "varsayılan" kılavuz görüntüününden sapdık.</span><span class="sxs-lookup"><span data-stu-id="848e6-147">Note that we have deviated from the "default" grid display by implementing three custom columns.</span></span>

<span data-ttu-id="848e6-148">Birincisi, miktar için düzenlenebilir, "bağlantılı" bir alandır:</span><span class="sxs-lookup"><span data-stu-id="848e6-148">The first is an Editable, "Bound" field for the Quantity:</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

<span data-ttu-id="848e6-149">Bir sonraki, satır öğe toplamı (sipariş edilecek miktar) gösteren "hesaplanan" bir sütundur:</span><span class="sxs-lookup"><span data-stu-id="848e6-149">The next is a "calculated" column that displays the line item total (the item cost times the quantity to be ordered):</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

<span data-ttu-id="848e6-150">Son olarak, kullanıcının öğenin alışveriş grafiğinden kaldırılması gerektiğini belirtmek için kullanacağı CheckBox denetimini içeren özel bir sütunu vardır.</span><span class="sxs-lookup"><span data-stu-id="848e6-150">Lastly we have a custom column that contains a CheckBox control that the user will use to indicate that the item should be removed from the shopping chart.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

<span data-ttu-id="848e6-151">Görebileceğiniz gibi, Order Total satırı boş olduğundan, sipariş toplamını hesaplamak için bir mantık ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="848e6-151">As you can see, the Order Total line is empty so let's add some logic to calculate the Order Total.</span></span>

<span data-ttu-id="848e6-152">Önce MyShoppingCart sınıfımızda bir "GetTotal" yöntemi uygulayacağız.</span><span class="sxs-lookup"><span data-stu-id="848e6-152">We'll first implement a "GetTotal" method to our MyShoppingCart Class.</span></span>

<span data-ttu-id="848e6-153">MyShoppingCart.cs dosyasında aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="848e6-153">In the MyShoppingCart.cs file add the following code.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

<span data-ttu-id="848e6-154">Daha sonra sayfa\_Load olay işleyicisine GetTotal yönteminizi çağırabiliriz.</span><span class="sxs-lookup"><span data-stu-id="848e6-154">Then in the Page\_Load event handler we'll can call our GetTotal method.</span></span> <span data-ttu-id="848e6-155">Aynı zamanda, alışveriş sepetinin boş olup olmadığını görmek için bir test ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="848e6-155">At the same time we'll add a test to see if the shopping cart is empty and adjust the display accordingly if it is.</span></span>

<span data-ttu-id="848e6-156">Şimdi alışveriş sepeti boşsa şunu ediniyoruz:</span><span class="sxs-lookup"><span data-stu-id="848e6-156">Now if the shopping cart is empty we get this:</span></span>

![](tailspin-spyworks-part-5/_static/image4.jpg)

<span data-ttu-id="848e6-157">Aksi takdirde, bizim toplamımızı görüyoruz.</span><span class="sxs-lookup"><span data-stu-id="848e6-157">And if not, we see our total.</span></span>

![](tailspin-spyworks-part-5/_static/image5.jpg)

<span data-ttu-id="848e6-158">Ancak, Bu sayfa henüz tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="848e6-158">However, this page is not yet complete.</span></span>

<span data-ttu-id="848e6-159">Kaldırma için işaretlenen öğeleri kaldırarak ve yeni miktar değerlerini belirleyerek, Kullanıcı tarafından kılavuzda değiştirilmiş olabileceğinden, alışveriş sepetini yeniden hesaplamak için ek mantığa ihtiyacımız olacak.</span><span class="sxs-lookup"><span data-stu-id="848e6-159">We will need additional logic to recalculate the shopping cart by removing items marked for removal and by determining new quantity values as some may have been changed in the grid by the user.</span></span>

<span data-ttu-id="848e6-160">Bir Kullanıcı bir öğeyi kaldırmak üzere işaretlediğinde durumu işlemek için MyShoppingCart.cs içindeki alışveriş sepeti sınıfımızın "RemoveItem" yöntemini eklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="848e6-160">Lets add a "RemoveItem" method to our shopping cart class in MyShoppingCart.cs to handle the case when a user marks an item for removal.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

<span data-ttu-id="848e6-161">Şimdi, bir Kullanıcı bir kaliteyi GridView 'da sipariş olacak şekilde değiştirdiğinde, bu, bir yöntemi ele alalım.</span><span class="sxs-lookup"><span data-stu-id="848e6-161">Now let's ad a method to handle the circumstance when a user simply changes the quality to be ordered in the GridView.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

<span data-ttu-id="848e6-162">Temel kaldırma ve güncelleştirme özellikleriyle birlikte, veritabanındaki alışveriş sepetini gerçekten güncelleştiren mantığı uygulayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="848e6-162">With the basic Remove and Update features in place we can implement the logic that actually updates the shopping cart in the database.</span></span> <span data-ttu-id="848e6-163">(MyShoppingCart.cs)</span><span class="sxs-lookup"><span data-stu-id="848e6-163">(In MyShoppingCart.cs)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

<span data-ttu-id="848e6-164">Bu yöntemin iki parametre beklediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="848e6-164">You'll note that this method expects two parameters.</span></span> <span data-ttu-id="848e6-165">Bunlardan biri, alışveriş sepeti kimliğidir ve diğeri Kullanıcı tanımlı türdeki nesnelerin bir dizisidir.</span><span class="sxs-lookup"><span data-stu-id="848e6-165">One is the shopping cart Id and the other is an array of objects of user defined type.</span></span>

<span data-ttu-id="848e6-166">Bu nedenle, Kullanıcı arabirimi özellikleri üzerinde mantığımız bağımlılığı en aza indirmek için, GridView denetimine doğrudan erişme gereksinimi olmadan, alışveriş sepeti öğelerini kodumuza iletmek üzere kullandığımız bir veri yapısı tanımladık.</span><span class="sxs-lookup"><span data-stu-id="848e6-166">So as to minimize the dependency of our logic on user interface specifics, we've defined a data structure that we can use to pass the shopping cart items to our code without our method needing to directly access the GridView control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

<span data-ttu-id="848e6-167">MyShoppingCart.aspx.cs dosyanızda, bu yapıyı Güncelleştir düğümüzde olay işleyicisi ' ne tıklayarak aşağıda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="848e6-167">In our MyShoppingCart.aspx.cs file we can use this structure in our Update Button Click Event handler as follows.</span></span> <span data-ttu-id="848e6-168">Sepet güncelleştirmesinin yanı sıra sepet toplamı da güncelleştirilecektir.</span><span class="sxs-lookup"><span data-stu-id="848e6-168">Note that in addition to updating the cart we will update the cart total as well.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

<span data-ttu-id="848e6-169">Bu kod satırıyla ilgili belirli bir ilgi olduğunu aklınızda edin:</span><span class="sxs-lookup"><span data-stu-id="848e6-169">Note with particular interest this line of code:</span></span>

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

<span data-ttu-id="848e6-170">GetValues (), MyShoppingCart.aspx.cs içinde aşağıdaki gibi uygulayacağız özel bir yardımcı işlevdir.</span><span class="sxs-lookup"><span data-stu-id="848e6-170">GetValues() is a special helper function that we will implement in MyShoppingCart.aspx.cs as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

<span data-ttu-id="848e6-171">Bu, GridView denetimizdeki bağlantılı öğelerin değerlerine erişmenin temiz bir yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="848e6-171">This provides a clean way to access the values of the bound elements in our GridView control.</span></span> <span data-ttu-id="848e6-172">"Öğe kaldır" onay kutusu denetimi bağlanmadı çünkü bu, FindControl () yöntemiyle erişeceğiz.</span><span class="sxs-lookup"><span data-stu-id="848e6-172">Since our "Remove Item" CheckBox Control is not bound we'll access it via the FindControl() method.</span></span>

<span data-ttu-id="848e6-173">Projenizin geliştirmesinde bu aşamada, kullanıma alma işlemini uygulamaya hazırız.</span><span class="sxs-lookup"><span data-stu-id="848e6-173">At this stage in your project's development we are getting ready to implement the checkout process.</span></span>

<span data-ttu-id="848e6-174">Bunu yapmadan önce, üyelik veritabanını oluşturmak ve üyelik deposuna bir kullanıcı eklemek için Visual Studio 'Yu kullanalım.</span><span class="sxs-lookup"><span data-stu-id="848e6-174">Before doing so let's use Visual Studio to generate the membership database and add a user to the membership repository.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="848e6-175">[Önceki](tailspin-spyworks-part-4.md)
> [İleri](tailspin-spyworks-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="848e6-175">[Previous](tailspin-spyworks-part-4.md)
[Next](tailspin-spyworks-part-6.md)</span></span>
