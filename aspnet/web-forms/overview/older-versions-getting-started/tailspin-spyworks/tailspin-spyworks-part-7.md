---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: '7\. Bölüm: özellik ekleme | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 7, hesap yeniden görünümü gibi ek özellikler ekler...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641997"
---
# <a name="part-7-adding-features"></a><span data-ttu-id="ffc95-104">7\. Bölüm: Özellik Ekleme</span><span class="sxs-lookup"><span data-stu-id="ffc95-104">Part 7: Adding Features</span></span>

<span data-ttu-id="ffc95-105">[ali Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="ffc95-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="ffc95-106">Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="ffc95-107">Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="ffc95-108">Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="ffc95-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="ffc95-109">Bölüm 7, hesap incelemesi, Ürün İncelemeleri ve "popüler öğeler" ve "Ayrıca satın alınan" Kullanıcı denetimleri gibi ek özellikler ekler.</span><span class="sxs-lookup"><span data-stu-id="ffc95-109">Part 7 adds additional features, such as account review, product reviews, and "popular items" and "also purchased" user controls.</span></span>

## <a id="_Toc260221673"></a><span data-ttu-id="ffc95-110">Özellik ekleme</span><span class="sxs-lookup"><span data-stu-id="ffc95-110">Adding Features</span></span>

<span data-ttu-id="ffc95-111">Kullanıcılar kataloğumuza göz atabiliyor, bunları kendi alışveriş sepetine yerleştirse ve kullanıma alma işlemini tamamlayabilse de, sitemizi geliştirmek için dahil ettiğimiz birçok destekleyici özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="ffc95-111">Though users can browse our catalog, place items in their shopping cart, and complete the checkout process, there are a number of supporting features that we will include to improve our site.</span></span>

1. <span data-ttu-id="ffc95-112">Hesap Incelemesi (verilen siparişleri listeleyin ve ayrıntıları görüntüleyin.)</span><span class="sxs-lookup"><span data-stu-id="ffc95-112">Account Review (List orders placed and view details.)</span></span>
2. <span data-ttu-id="ffc95-113">İlk sayfaya belirli bir içeriğe özgü içerik ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ffc95-113">Add some context specific content to the front page.</span></span>
3. <span data-ttu-id="ffc95-114">Kullanıcıların katalogdaki ürünleri Incelemesine izin vermek için bir özellik ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ffc95-114">Add a feature to let users Review the products in the catalog.</span></span>
4. <span data-ttu-id="ffc95-115">Popüler öğeleri göstermek ve bu denetimi ön sayfaya yerleştirmek için bir kullanıcı denetimi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ffc95-115">Create a User Control to display Popular Items and Place that control on the front page.</span></span>
5. <span data-ttu-id="ffc95-116">"Ayrıca satın alınmış" Kullanıcı denetimi oluşturun ve ürün ayrıntıları sayfasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ffc95-116">Create an "Also Purchased" user control and add it to the product details page.</span></span>
6. <span data-ttu-id="ffc95-117">Kişi sayfası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ffc95-117">Add a Contact Page.</span></span>
7. <span data-ttu-id="ffc95-118">Hakkında bir sayfa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ffc95-118">Add an About Page.</span></span>
8. <span data-ttu-id="ffc95-119">Genel hata</span><span class="sxs-lookup"><span data-stu-id="ffc95-119">Global Error</span></span>

## <a id="_Toc260221674"></a><span data-ttu-id="ffc95-120">Hesap Incelemesi</span><span class="sxs-lookup"><span data-stu-id="ffc95-120">Account Review</span></span>

<span data-ttu-id="ffc95-121">"Account" klasöründe, farklı bir OrderList. aspx adlı ve diğer adlandırılmış OrderDetails. aspx adlı iki. aspx sayfası oluşturun</span><span class="sxs-lookup"><span data-stu-id="ffc95-121">In the "Account" folder create two .aspx pages one named OrderList.aspx and the other named OrderDetails.aspx</span></span>

<span data-ttu-id="ffc95-122">OrderList. aspx, daha önce yaptığımız gibi GridView ve EntityDataSource denetimlerinden faydalanır.</span><span class="sxs-lookup"><span data-stu-id="ffc95-122">OrderList.aspx will leverage the GridView and EntityDataSource controls much as we have previously.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

<span data-ttu-id="ffc95-123">EntityDataSource, Kullanıcı oturumunun oturum açması sırasında bir oturum değişkeninde belirlediğimiz Kullanıcı adında (burada, bkz. parametre) filtrelenmiş Orders tablosundan kayıtlar seçer.</span><span class="sxs-lookup"><span data-stu-id="ffc95-123">The EntityDataSource selects records from the Orders table filtered on the UserName (see the WhereParameter) which we set in a session variable when the user log's in.</span></span>

<span data-ttu-id="ffc95-124">GridView 'un Hyperlinkalanındaki bu parametreleri de göz önünde bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ffc95-124">Note also these parameters in the HyperlinkField of the GridView:</span></span>

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

<span data-ttu-id="ffc95-125">Bu, OrderDetails. aspx sayfasına bir QueryString parametresi olarak OrderID alanını belirten her ürün için sipariş ayrıntıları görünümünün bağlantısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-125">These specify the link to the Order details view for each product specifying the OrderID field as a QueryString parameter to the OrderDetails.aspx page.</span></span>

## <a id="_Toc260221675"></a><span data-ttu-id="ffc95-126">OrderDetails. aspx</span><span class="sxs-lookup"><span data-stu-id="ffc95-126">OrderDetails.aspx</span></span>

<span data-ttu-id="ffc95-127">Siparişe ve bir FormView 'a erişmek için bir EntityDataSource denetimi kullanacağız ve tüm sipariş satır öğelerini görüntüleyen bir GridView ile başka bir EntityDataSource 'a sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-127">We will use an EntityDataSource control to access the Orders and a FormView to display the Order data and another EntityDataSource with a GridView to display all the Order's line items.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

<span data-ttu-id="ffc95-128">Arka plan kodu dosyasında (OrderDetails.aspx.cs), iki adet evetme tutuyoruz.</span><span class="sxs-lookup"><span data-stu-id="ffc95-128">In the Code Behind file (OrderDetails.aspx.cs) we have two little bits of housekeeping.</span></span>

<span data-ttu-id="ffc95-129">İlk olarak OrderDetails 'in her zaman bir OrderID aldığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-129">First we need to make sure that OrderDetails always gets an OrderId.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

<span data-ttu-id="ffc95-130">Ayrıca, satır öğelerinden sipariş toplamını hesaplamakta ve görüntüleriz.</span><span class="sxs-lookup"><span data-stu-id="ffc95-130">We also need to calculate and display the order total from the line items.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a><span data-ttu-id="ffc95-131">Giriş sayfası</span><span class="sxs-lookup"><span data-stu-id="ffc95-131">The Home Page</span></span>

<span data-ttu-id="ffc95-132">Default. aspx sayfasına bazı statik içerik ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="ffc95-132">Let's add some static content to the Default.aspx page.</span></span>

<span data-ttu-id="ffc95-133">İlk olarak bir "Içerik" klasörü ve bir Resimler klasörü oluşturacak (ana sayfada kullanılacak bir görüntü de ekleyeceğiz.)</span><span class="sxs-lookup"><span data-stu-id="ffc95-133">First I'll create a "Content" folder and within it an Images folder (and I'll include an image to be used on the home page.)</span></span>

<span data-ttu-id="ffc95-134">Default. aspx sayfasının en alt yer tutucusuna aşağıdaki biçimlendirmeyi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ffc95-134">Into the bottom placeholder of the Default.aspx page, add the following markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a><span data-ttu-id="ffc95-135">Ürün Incelemeleri</span><span class="sxs-lookup"><span data-stu-id="ffc95-135">Product Reviews</span></span>

<span data-ttu-id="ffc95-136">İlk olarak, bir ürün incelemesi girmek için kullandığımız bir formun bağlantısını içeren bir düğme ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="ffc95-136">First we'll add a button with a link to a form that we can use to enter a product review.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

<span data-ttu-id="ffc95-137">ProductID 'yi sorgu dizesinde geçirdiğimiz unutulmamalıdır</span><span class="sxs-lookup"><span data-stu-id="ffc95-137">Note that we are passing the ProductID in the query string</span></span>

<span data-ttu-id="ffc95-138">Daha sonra, BelgeAdı \ Add. aspx adlı sayfayı ekleyelim</span><span class="sxs-lookup"><span data-stu-id="ffc95-138">Next let's add page named ReviewAdd.aspx</span></span>

<span data-ttu-id="ffc95-139">Bu sayfa, ASP.NET AJAX denetim araç setini kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="ffc95-139">This page will use the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="ffc95-140">Daha önce yapmadıysanız, [DevExpress](http://devexpress.com/act) 'den indirebilirsiniz ve burada [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)Visual Studio ile kullanmak üzere araç takımını ayarlamaya yönelik yönergeler vardır.</span><span class="sxs-lookup"><span data-stu-id="ffc95-140">If you have not already done so you can download it from [DevExpress](http://devexpress.com/act) and there is guidance on setting up the toolkit for use with Visual Studio here [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md).</span></span>

<span data-ttu-id="ffc95-141">Tasarım modunda, araç kutusu ' ndan denetimleri ve Doğrulayıcıları sürükleyin ve aşağıdaki gibi bir form oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ffc95-141">In design mode, drag controls and validators from the toolbox and build a form like the one below.</span></span>

![](tailspin-spyworks-part-7/_static/image2.jpg)

<span data-ttu-id="ffc95-142">Biçimlendirme şuna benzer şekilde görünecektir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-142">The markup will look something like this.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

<span data-ttu-id="ffc95-143">İncelemeleri girebilmemiz için artık bu İncelemeleri ürün sayfasında görüntülemesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ffc95-143">Now that we can enter reviews, lets display those reviews on the product page.</span></span>

<span data-ttu-id="ffc95-144">Bu biçimlendirmeyi ProductDetails. aspx sayfasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ffc95-144">Add this markup to the ProductDetails.aspx page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

<span data-ttu-id="ffc95-145">Uygulamamızı şimdi çalıştırmak ve bir ürüne gitmek, müşteri incelemeleri dahil ürün bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-145">Running our application now and navigating to a product shows the product information including customer reviews.</span></span>

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a><span data-ttu-id="ffc95-146">Popüler öğeler denetimi (Kullanıcı denetimleri oluşturma)</span><span class="sxs-lookup"><span data-stu-id="ffc95-146">Popular Items Control (Creating User Controls)</span></span>

<span data-ttu-id="ffc95-147">Web sitenizdeki satışları artırmak için, "müstehcen satış" popüler veya ilgili ürünlere birkaç özellik ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="ffc95-147">In order to increase sales on your web site we will add a couple of features to "suggestive sell" popular or related products.</span></span>

<span data-ttu-id="ffc95-148">Bu özelliklerden ilki, ürün kataloğumuza ait daha popüler ürünün bir listesi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ffc95-148">The first of these features will be a list of the more popular product in our product catalog.</span></span>

<span data-ttu-id="ffc95-149">Uygulamamızın giriş sayfasında en çok satılan öğeleri göstermek için bir "Kullanıcı denetimi" oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="ffc95-149">We will create a "User Control" to display the top selling items on the home page of our application.</span></span> <span data-ttu-id="ffc95-150">Bu bir denetim olacağı için, Visual Studio tasarımcısında denetimi istediğiniz herhangi bir sayfada sürükleyip bırakarak bu denetimi herhangi bir sayfada kullanabiliriz.</span><span class="sxs-lookup"><span data-stu-id="ffc95-150">Since this will be a control, we can use it on any page by simply dragging and dropping the control in Visual Studio's designer onto any page that we like.</span></span>

<span data-ttu-id="ffc95-151">Visual Studio 'nun Çözüm Gezgini ' nde çözüm adına sağ tıklayın ve "denetimler" adlı yeni bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ffc95-151">In Visual Studio's solutions explorer, right-click on the solution name and create a new directory named "Controls".</span></span> <span data-ttu-id="ffc95-152">Bunun yapılması gerekli olmasa da, "denetimler" dizinindeki tüm Kullanıcı denetimlerimizi oluşturarak projemizi düzenli tutmaya yardımcı olacak.</span><span class="sxs-lookup"><span data-stu-id="ffc95-152">While it is not necessary to do so, we will help keep our project organized by creating all our user controls in the "Controls" directory.</span></span>

<span data-ttu-id="ffc95-153">Denetimler klasörüne sağ tıklayın ve "yeni öğe" yi seçin:</span><span class="sxs-lookup"><span data-stu-id="ffc95-153">Right-click on the controls folder and choose "New Item" :</span></span>

![](tailspin-spyworks-part-7/_static/image4.jpg)

<span data-ttu-id="ffc95-154">"Popularıtems" denetiimizin bir adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="ffc95-154">Specify a name for our control of "PopularItems".</span></span> <span data-ttu-id="ffc95-155">Kullanıcı denetimleri için dosya uzantısının. ascx değil. aspx olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ffc95-155">Note that the file extension for user controls is .ascx not .aspx.</span></span>

<span data-ttu-id="ffc95-156">Popüler öğelerimiz Kullanıcı denetimi, aşağıdaki gibi tanımlanacak.</span><span class="sxs-lookup"><span data-stu-id="ffc95-156">Our Popular Items User control will be defined as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

<span data-ttu-id="ffc95-157">Burada, bu uygulamada henüz kullandığımız bir yöntemi kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="ffc95-157">Here we're using a method we have not used yet in this application.</span></span> <span data-ttu-id="ffc95-158">Yineleyici denetimini kullandık ve bir veri kaynağı denetimi kullanmak yerine, yineleyici denetimini bir LINQ to Entities sorgusunun sonuçlarına bağlamamız yapıyoruz.</span><span class="sxs-lookup"><span data-stu-id="ffc95-158">We're using the repeater control and instead of using a data source control we're binding the Repeater Control to the results of a LINQ to Entities query.</span></span>

<span data-ttu-id="ffc95-159">Denetiminizin arkasındaki kodda aşağıdaki gibi yaptık.</span><span class="sxs-lookup"><span data-stu-id="ffc95-159">In the code behind of our control we do that as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

<span data-ttu-id="ffc95-160">Ayrıca Denetim işaretimizin en üstündeki bu önemli satırı göz önünde bulundurulın.</span><span class="sxs-lookup"><span data-stu-id="ffc95-160">Note also this important line at the top of our control's markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

<span data-ttu-id="ffc95-161">En popüler öğeler dakika temelinde değiştirilmeyeceği için uygulamamız performansını artırmak üzere bir aching yönergesi ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="ffc95-161">Since the most popular items won't be changing on a minute to minute basis we can add a aching directive to improve the performance of our application.</span></span> <span data-ttu-id="ffc95-162">Bu yönerge, Denetim kodunun yalnızca, denetimin önbelleğe alınan çıktısı zaman aşımına uğradığında yürütülmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="ffc95-162">This directive will cause the controls code to only be executed when the cached output of the control expires.</span></span> <span data-ttu-id="ffc95-163">Aksi takdirde, denetimin çıktısının önbelleğe alınmış sürümü kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="ffc95-163">Otherwise, the cached version of the control's output will be used.</span></span>

<span data-ttu-id="ffc95-164">Şimdi yaptığımız tek şey, default. aspx sayfamızda yeni denetimimizi içerir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-164">Now all we have to do is include our new control in our Default.aspx page.</span></span>

<span data-ttu-id="ffc95-165">Bir denetimin örneğini varsayılan formumuzu Aç sütununa yerleştirmek için sürükle ve bırak öğesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ffc95-165">Use drag and drop to place an instance of the control in the open column of our Default form.</span></span>

![](tailspin-spyworks-part-7/_static/image5.jpg)

<span data-ttu-id="ffc95-166">Uygulamamızı çalıştırdığımızda, giriş sayfasında en popüler öğeler görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-166">Now when we run our application the home page displays the most popular items.</span></span>

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a><span data-ttu-id="ffc95-167">"Ayrıca satın alınan" denetim (parametrelerle Kullanıcı denetimleri)</span><span class="sxs-lookup"><span data-stu-id="ffc95-167">"Also Purchased" Control (User Controls with Parameters)</span></span>

<span data-ttu-id="ffc95-168">Oluşturacağımız ikinci Kullanıcı denetimi, bağlam özelliği ekleyerek bir sonraki düzeye göre daha fazla satıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ffc95-168">The second User Control that we'll create will take suggestive selling to the next level by adding context specificity.</span></span>

<span data-ttu-id="ffc95-169">En üstteki "Ayrıca satın alınan" öğeleri hesaplama mantığı önemsiz değildir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-169">The logic to calculate the top "Also Purchased" items is non-trivial.</span></span>

<span data-ttu-id="ffc95-170">"Ayrıca satın almış olan" denetim, seçili olan ProductID için OrderDetails kayıtlarını (daha önce satın alınan) seçer ve bulunan her benzersiz sipariş için OrderID 'leri alacak.</span><span class="sxs-lookup"><span data-stu-id="ffc95-170">Our "Also Purchased" control will select the OrderDetails records (previously purchased) for the currently selected ProductID and grab the OrderIDs for each unique order that is found.</span></span>

<span data-ttu-id="ffc95-171">Ardından, tüm bu siparişlerden ürünleri Al ' ı seçeceğiz ve satın alınan miktarları toplammız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-171">Then we will select al the products from all those Orders and sum the quantities purchased.</span></span> <span data-ttu-id="ffc95-172">Ürünleri bu miktar toplamına göre sıralayacak ve ilk beş öğeyi görüntüleyecek.</span><span class="sxs-lookup"><span data-stu-id="ffc95-172">We'll sort the products by that quantity sum and display the top five items.</span></span>

<span data-ttu-id="ffc95-173">Bu mantığın karmaşıklığı verildiğinde, bu algoritmayı saklı yordam olarak uygulayacağız.</span><span class="sxs-lookup"><span data-stu-id="ffc95-173">Given the complexity of this logic, we will implement this algorithm as a stored procedure.</span></span>

<span data-ttu-id="ffc95-174">Saklı yordam için T-SQL aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-174">The T-SQL for the stored procedure is as follows.</span></span>

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

<span data-ttu-id="ffc95-175">Bu saklı yordamın (SelectPurchasedWithProducts) uygulamamıza dahil ettiğimiz sırada olduğunu ve belirttiğimiz Varlık Veri Modeli oluşturduğumuzdan, gereken tablo ve görünümlere ek olarak, Varlık Veri Modeli Bu saklı yordamı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-175">Note that this stored procedure (SelectPurchasedWithProducts) existed in the database when we included it in our application and when we generated the Entity Data Model we specified that, in addition to the Tables and Views that we needed, the Entity Data Model should include this stored procedure.</span></span>

<span data-ttu-id="ffc95-176">Saklı yordama Varlık Veri Modeli erişmek için, işlevi içeri aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-176">To access the stored procedure from the Entity Data Model we need to import the function.</span></span>

<span data-ttu-id="ffc95-177">Çözüm Gezgini 'ndeki Varlık Veri Modeli çift tıklayarak tasarımcıda açın ve model tarayıcısını açın, sonra tasarımcıya sağ tıklayıp "Işlev Içeri aktarma Ekle" seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="ffc95-177">Double Click on the Entity Data Model in the Solutions Explorer to open it in the designer and open the Model Browser, then right-click in the designer and select "Add Function Import".</span></span>

![](tailspin-spyworks-part-7/_static/image1.png)

<span data-ttu-id="ffc95-178">Bu işlem, bu iletişim kutusunu açar.</span><span class="sxs-lookup"><span data-stu-id="ffc95-178">Doing so will open this dialog.</span></span>

![](tailspin-spyworks-part-7/_static/image2.png)

<span data-ttu-id="ffc95-179">Yukarıda gördüğünüz gibi alanları doldurun, "SelectPurchasedWithProducts" öğesini seçin ve içeri aktarılan işlevimizin adı için yordam adını kullanın.</span><span class="sxs-lookup"><span data-stu-id="ffc95-179">Fill out the fields as you see above, selecting the "SelectPurchasedWithProducts" and use the procedure name for the name of our imported function.</span></span>

<span data-ttu-id="ffc95-180">"Tamam" a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ffc95-180">Click "Ok".</span></span>

<span data-ttu-id="ffc95-181">Bunu yaptıktan sonra, modeldeki başka herhangi bir öğe olabileceğinden, saklı yordama göre programlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ffc95-181">Having done this we can simply program against the stored procedure as we might any other item in the model.</span></span>

<span data-ttu-id="ffc95-182">Bu nedenle, "denetimlerimiz" klasöründe AlsoPurchased. ascx adlı yeni bir kullanıcı denetimi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ffc95-182">So, in our "Controls" folder create a new user control named AlsoPurchased.ascx.</span></span>

<span data-ttu-id="ffc95-183">Bu denetimin biçimlendirmesi, Popularıtems denetimine çok tanıdık gelecektir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-183">The markup for this control will look very familiar to the PopularItems control.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

<span data-ttu-id="ffc95-184">Önemli farkı, öğenin işlenmesi, ürüne göre farklı olacağı için çıktıyı önbelleğe alma işlemlerdir.</span><span class="sxs-lookup"><span data-stu-id="ffc95-184">The notable difference is that are not caching the output since the item's to be rendered will differ by product.</span></span>

<span data-ttu-id="ffc95-185">ProductID, denetimin bir "özelliği" olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ffc95-185">The ProductId will be a "property" to the control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

<span data-ttu-id="ffc95-186">Denetimin PreRender olay işleyicisinde üç şey yapmak için göz yorduk.</span><span class="sxs-lookup"><span data-stu-id="ffc95-186">In the control's PreRender event handler we eed to do three things.</span></span>

1. <span data-ttu-id="ffc95-187">ProductID 'nin ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="ffc95-187">Make sure the ProductID is set.</span></span>
2. <span data-ttu-id="ffc95-188">Geçerli bir ürünle satın alınmış ürünler olup olmadığını görün.</span><span class="sxs-lookup"><span data-stu-id="ffc95-188">See if there are any products that have been purchased with the current one.</span></span>
3. <span data-ttu-id="ffc95-189">Bazı öğelerin #2 belirlendiği şekilde çıkışını yapın.</span><span class="sxs-lookup"><span data-stu-id="ffc95-189">Output some items as determined in #2.</span></span>

<span data-ttu-id="ffc95-190">Saklı yordamı model aracılığıyla çağırmanın ne kadar kolay olduğunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ffc95-190">Note how easy it is to call the stored procedure through the model.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

<span data-ttu-id="ffc95-191">"Ayrıca satın alındı" olduğunu belirlemekten sonra, yineleyicisi 'ni sorgu tarafından döndürülen sonuçlara bağlayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="ffc95-191">After determining that there ARE "also purchased" we can simply bind the repeater to the results returned by the query.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

<span data-ttu-id="ffc95-192">"Ayrıca satın alınmış" öğeler yoksa kataloğumuzdan diğer popüler öğeleri görüntüleriz.</span><span class="sxs-lookup"><span data-stu-id="ffc95-192">If there were not any "also purchased" items we'll simply display other popular items from our catalog.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

<span data-ttu-id="ffc95-193">"Ayrıca satın alınan" öğeleri görüntülemek için ProductDetails. aspx sayfasını açın ve AlsoPurchased denetimini, bu konumda görünmesini sağlamak üzere Çözüm Gezgini 'nden sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="ffc95-193">To view the "Also Purchased" items, open the ProductDetails.aspx page and drag the AlsoPurchased control from the Solutions Explorer so that it appears in this position in the markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

<span data-ttu-id="ffc95-194">Bu işlem, ProductDetails sayfasının en üstünde bulunan denetime bir başvuru oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ffc95-194">Doing so will create a reference to the control at the top of the ProductDetails page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

<span data-ttu-id="ffc95-195">AlsoPurchased Kullanıcı denetimi bir ProductID numarası gerektirdiğinden, sayfanın geçerli veri modeli öğesine karşı bir eval ekstresi kullanarak denetimizin ProductID özelliğini ayarlayacağız.</span><span class="sxs-lookup"><span data-stu-id="ffc95-195">Since the AlsoPurchased user control requires a ProductId number we will set the ProductID property of our control by using an Eval statement against the current data model item of the page.</span></span>

![](tailspin-spyworks-part-7/_static/image3.png)

<span data-ttu-id="ffc95-196">Şimdi oluşturup çalıştırdığımızda bir ürüne gözattığınızda, "Ayrıca satın alındı" öğelerini görtik.</span><span class="sxs-lookup"><span data-stu-id="ffc95-196">When we build and run now and browse to a product we see the "Also Purchased" items.</span></span>

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> <span data-ttu-id="ffc95-197">[Önceki](tailspin-spyworks-part-6.md)
> [İleri](tailspin-spyworks-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="ffc95-197">[Previous](tailspin-spyworks-part-6.md)
[Next](tailspin-spyworks-part-8.md)</span></span>
