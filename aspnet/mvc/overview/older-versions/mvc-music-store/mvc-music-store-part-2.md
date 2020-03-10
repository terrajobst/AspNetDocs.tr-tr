---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: '2\. Bölüm: denetleyiciler | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 2\. Bölüm denetleyicileri içerir.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559880"
---
# <a name="part-2-controllers"></a><span data-ttu-id="c2e3f-104">2\. Bölüm: Denetleyiciler</span><span class="sxs-lookup"><span data-stu-id="c2e3f-104">Part 2: Controllers</span></span>

<span data-ttu-id="c2e3f-105">[Jon Galloway](https://github.com/jongalloway) tarafından</span><span class="sxs-lookup"><span data-stu-id="c2e3f-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="c2e3f-106">MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="c2e3f-107">MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="c2e3f-108">Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="c2e3f-109">2\. Bölüm denetleyicileri içerir.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-109">Part 2 covers Controllers.</span></span>

<span data-ttu-id="c2e3f-110">Geleneksel Web çerçeveleri ile gelen URL 'Ler genellikle disk üzerindeki dosyalarla eşleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-110">With traditional web frameworks, incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="c2e3f-111">Örneğin: "/Products.aspx" veya "/Products.php" gibi bir URL isteği bir "Products. aspx" veya "Products. php" dosyası tarafından işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="c2e3f-112">Web tabanlı MVC çerçeveleri, URL 'Leri sunucu koduna biraz farklı bir şekilde eşler.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="c2e3f-113">Gelen URL 'Leri dosyalara eşlemek yerine, URL 'Leri sınıfların yöntemlerine eşleyin.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="c2e3f-114">Bu sınıflar "denetleyiciler" olarak adlandırılır ve gelen HTTP isteklerini işlemekten, Kullanıcı girişi işleme, verileri alma ve kaydetme ve istemciye geri gönderme yanıtını belirleme (HTML görüntüleme, bir dosyayı indirme, farklı bir şekilde yeniden yönlendirme) URL, vb.).</span><span class="sxs-lookup"><span data-stu-id="c2e3f-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span>

## <a name="adding-a-homecontroller"></a><span data-ttu-id="c2e3f-115">HomeController ekleme</span><span class="sxs-lookup"><span data-stu-id="c2e3f-115">Adding a HomeController</span></span>

<span data-ttu-id="c2e3f-116">Sitemizin ana sayfasında URL 'Leri işleyecek bir denetleyici sınıfı ekleyerek MVC müzik deposu uygulamamıza başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-116">We'll begin our MVC Music Store application by adding a Controller class that will handle URLs to the Home page of our site.</span></span> <span data-ttu-id="c2e3f-117">ASP.NET MVC 'nin varsayılan adlandırma kurallarını takip edeceğiz ve HomeController ' a çağrı yapacağız.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-117">We'll follow the default naming conventions of ASP.NET MVC and call it HomeController.</span></span>

<span data-ttu-id="c2e3f-118">Çözüm Gezgini içindeki "denetleyiciler" klasörüne sağ tıklayın ve "Ekle" yi ve ardından "denetleyici..." öğesini seçin. komutundaki</span><span class="sxs-lookup"><span data-stu-id="c2e3f-118">Right-click the "Controllers" folder within the Solution Explorer and select "Add", and then the "Controller…" command:</span></span>

![](mvc-music-store-part-2/_static/image1.jpg)

<span data-ttu-id="c2e3f-119">Bu, "denetleyici Ekle" iletişim kutusunu getirir.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-119">This will bring up the "Add Controller" dialog.</span></span> <span data-ttu-id="c2e3f-120">Denetleyiciyi "HomeController" olarak adlandırın ve Ekle düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-120">Name the controller "HomeController" and press the Add button.</span></span>

![](mvc-music-store-part-2/_static/image1.png)

<span data-ttu-id="c2e3f-121">Bu, aşağıdaki kodla yeni bir HomeController.cs dosyası oluşturur:</span><span class="sxs-lookup"><span data-stu-id="c2e3f-121">This will create a new file, HomeController.cs, with the following code:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

<span data-ttu-id="c2e3f-122">Mümkün olduğunca basit bir şekilde başlamak için Dizin metodunu yalnızca bir dize döndüren basit bir yöntemle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-122">To start as simply as possible, let's replace the Index method with a simple method that just returns a string.</span></span> <span data-ttu-id="c2e3f-123">İki değişiklik yapacağız:</span><span class="sxs-lookup"><span data-stu-id="c2e3f-123">We'll make two changes:</span></span>

- <span data-ttu-id="c2e3f-124">Yöntemi eylem sonucu yerine bir dize döndürecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="c2e3f-124">Change the method to return a string instead of an ActionResult</span></span>
- <span data-ttu-id="c2e3f-125">Return ifadesini "from evden" döndürecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="c2e3f-125">Change the return statement to return "Hello from Home"</span></span>

<span data-ttu-id="c2e3f-126">Yöntemi şu şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="c2e3f-126">The method should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a><span data-ttu-id="c2e3f-127">Uygulamayı Çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c2e3f-127">Running the Application</span></span>

<span data-ttu-id="c2e3f-128">Şimdi siteyi çalıştıralım.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-128">Now let's run the site.</span></span> <span data-ttu-id="c2e3f-129">Web-Server ' i başlatabiliriz ve aşağıdakilerden birini kullanarak siteyi deneyebiliriz::</span><span class="sxs-lookup"><span data-stu-id="c2e3f-129">We can start our web-server and try out the site using any of the following::</span></span>

- <span data-ttu-id="c2e3f-130">Debug ⇨ start hata ayıklamayı Başlat menü öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="c2e3f-130">Choose the Debug ⇨ Start Debugging menu item</span></span>
- <span data-ttu-id="c2e3f-131">Araç çubuğundaki yeşil ok düğmesine tıklayın ![](mvc-music-store-part-2/_static/image2.jpg)</span><span class="sxs-lookup"><span data-stu-id="c2e3f-131">Click the Green arrow button in the toolbar ![](mvc-music-store-part-2/_static/image2.jpg)</span></span>
- <span data-ttu-id="c2e3f-132">F5 klavye kısayolunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-132">Use the keyboard shortcut, F5.</span></span>

<span data-ttu-id="c2e3f-133">Yukarıdaki adımlardan herhangi birini kullanmak, projemizi derler ve Visual Web Developer 'ın yerleşik ASP.NET geliştirme sunucusunun başlatılmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-133">Using any of the above steps will compile our project, and then cause the ASP.NET Development Server that is built-into Visual Web Developer to start.</span></span> <span data-ttu-id="c2e3f-134">ASP.NET Development Server 'ın başlatıldığını göstermek için ekranın alt köşesinde bir bildirim görünür ve altında çalıştığı bağlantı noktası numarasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-134">A notification will appear in the bottom corner of the screen to indicate that the ASP.NET Development Server has started up, and will show the port number that it is running under.</span></span>

![](mvc-music-store-part-2/_static/image2.png)

<span data-ttu-id="c2e3f-135">Visual Web Developer, URL 'SI Web-Server ' ı işaret eden bir tarayıcı penceresini otomatik olarak açar.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-135">Visual Web Developer will then automatically open a browser window whose URL points to our web-server.</span></span> <span data-ttu-id="c2e3f-136">Bu, Web uygulamamızı hızlıca denememize olanak sağlayacak:</span><span class="sxs-lookup"><span data-stu-id="c2e3f-136">This will allow us to quickly try out our web application:</span></span>

![](mvc-music-store-part-2/_static/image3.png)

<span data-ttu-id="c2e3f-137">Neredeyse hızlı bir şekilde, yeni bir Web sitesi oluşturdunuz, üç satırlık bir işlev ekledik ve bir tarayıcıda metin aldık.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-137">Okay, that was pretty quick – we created a new website, added a three line function, and we've got text in a browser.</span></span> <span data-ttu-id="c2e3f-138">Roket bilimi değil, ancak bir başlangıç.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-138">Not rocket science, but it's a start.</span></span>

<span data-ttu-id="c2e3f-139">*Note: Visual Web Developer, Web sitenizi rastgele boş bir "bağlantı noktası" numarası üzerinde çalıştıracak ASP.NET geliştirme sunucusunu içerir. Yukarıdaki ekran görüntüsünde, site `http://localhost:26641/`çalışıyor, bu nedenle 26641 numaralı bağlantı noktasını kullanıyor. Bağlantı noktası numaranız farklı olacaktır. Bu öğreticide, URL 'ler gibi/Store/gözatım gibi bir iletişim kurduğumuz zaman, bağlantı noktası numarasından sonra da devam edecektir. 26641 numaralı bağlantı noktası,/Store/gözatma 'ya göz atarak `http://localhost:26641/Store/Browse`göz atacaktır.*</span><span class="sxs-lookup"><span data-stu-id="c2e3f-139">*Note: Visual Web Developer includes the ASP.NET Development Server, which will run your website on a random free "port" number. In the screenshot above, the site is running at `http://localhost:26641/`, so it's using port 26641. Your port number will be different. When we talk about URL's like /Store/Browse in this tutorial, that will go after the port number. Assuming a port number of 26641, browsing to /Store/Browse will mean browsing to `http://localhost:26641/Store/Browse`.*</span></span>

## <a name="adding-a-storecontroller"></a><span data-ttu-id="c2e3f-140">StoreController ekleme</span><span class="sxs-lookup"><span data-stu-id="c2e3f-140">Adding a StoreController</span></span>

<span data-ttu-id="c2e3f-141">Sitemizin ana sayfasını uygulayan basit bir HomeController ekledik.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-141">We added a simple HomeController that implements the Home Page of our site.</span></span> <span data-ttu-id="c2e3f-142">Şimdi, müzik mağazamız için göz atma işlevini uygulamak üzere kullanacağımız başka bir denetleyici ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-142">Let's now add another controller that we'll use to implement the browsing functionality of our music store.</span></span> <span data-ttu-id="c2e3f-143">Mağaza denetleyicimiz üç senaryoyu destekleyecektir:</span><span class="sxs-lookup"><span data-stu-id="c2e3f-143">Our store controller will support three scenarios:</span></span>

- <span data-ttu-id="c2e3f-144">Müzik mağazamız içindeki müzik tarzlarımızın bir listeleme sayfası</span><span class="sxs-lookup"><span data-stu-id="c2e3f-144">A listing page of the music genres in our music store</span></span>
- <span data-ttu-id="c2e3f-145">Belirli bir tarz tüm müzik albümlerini listeleyen bir tarayıcı sayfası</span><span class="sxs-lookup"><span data-stu-id="c2e3f-145">A browse page that lists all of the music albums in a particular genre</span></span>
- <span data-ttu-id="c2e3f-146">Belirli bir müzik albümünden ilgili bilgileri gösteren Ayrıntılar sayfası</span><span class="sxs-lookup"><span data-stu-id="c2e3f-146">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="c2e3f-147">Yeni bir StoreController sınıfı ekleyerek başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-147">We'll start by adding a new StoreController class..</span></span> <span data-ttu-id="c2e3f-148">Henüz yapmadıysanız, tarayıcıyı kapatarak veya Debug ⇨ Stop Debugging menü öğesini seçerek uygulamayı çalıştırmayı durdurun.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-148">If you haven't already, stop running the application either by closing the browser or selecting the Debug ⇨ Stop Debugging menu item.</span></span>

<span data-ttu-id="c2e3f-149">Şimdi yeni bir StoreController ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-149">Now add a new StoreController.</span></span> <span data-ttu-id="c2e3f-150">HomeController ile yaptığımız gibi, bunu, Çözüm Gezgini içinde "denetleyiciler" klasörüne sağ tıklayıp, Add-&gt;Controller menü öğesini seçerek yapacağız.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-150">Just like we did with HomeController, we'll do this by right-clicking on the "Controllers" folder within the Solution Explorer and choosing the Add-&gt;Controller menu item</span></span>

![](mvc-music-store-part-2/_static/image4.png)

<span data-ttu-id="c2e3f-151">Yeni StoreController bir "Dizin" metoduna zaten sahip.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-151">Our new StoreController already has an "Index" method.</span></span> <span data-ttu-id="c2e3f-152">Bu "Dizin" yöntemini, müzik Deponuzdaki tüm tarzları listeleyen listeleme sayfamızı uygulamak için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-152">We'll use this "Index" method to implement our listing page that lists all genres in our music store.</span></span> <span data-ttu-id="c2e3f-153">Ayrıca, StoreController 'ın işlemesini istediğimiz iki senaryoyu uygulamak için iki ek yöntem de ekleyeceğiz: tarama ve ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-153">We'll also add two additional methods to implement the two other scenarios we want our StoreController to handle: Browse and Details.</span></span>

<span data-ttu-id="c2e3f-154">Denetleyicimiz içindeki bu yöntemlere (Dizin, gözatmayı ve ayrıntıları) "denetleyici eylemleri" adı verilir ve HomeController. Index () eylem yöntemiyle zaten gördüğünüz gibi, işleri URL isteklerine yanıt verebiliyor ve (genel olarak konuşulur) hangi içeriğin olduğunu belirleme URL 'YI çağıran tarayıcıya veya kullanıcıya geri gönderilmelidir.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-154">These methods (Index, Browse and Details) within our Controller are called "Controller Actions", and as you've already seen with the HomeController.Index()action method, their job is to respond to URL requests and (generally speaking) determine what content should be sent back to the browser or user that invoked the URL.</span></span>

<span data-ttu-id="c2e3f-155">Dizin () yöntemini "Hello. Index ()" dizesini döndürecek şekilde değiştirerek StoreController uygulamamıza başlayacağız ve gözatıp () ve ayrıntılar () için benzer yöntemler ekleyeceğiz:</span><span class="sxs-lookup"><span data-stu-id="c2e3f-155">We'll start our StoreController implementation by changing theIndex() method to return the string "Hello from Store.Index()" and we'll add similar methods for Browse() and Details():</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

<span data-ttu-id="c2e3f-156">Projeyi yeniden çalıştırın ve aşağıdaki URL 'Lere gözatamazsınız:</span><span class="sxs-lookup"><span data-stu-id="c2e3f-156">Run the project again and browse the following URLs:</span></span>

- <span data-ttu-id="c2e3f-157">/Store</span><span class="sxs-lookup"><span data-stu-id="c2e3f-157">/Store</span></span>
- <span data-ttu-id="c2e3f-158">/Store/zat</span><span class="sxs-lookup"><span data-stu-id="c2e3f-158">/Store/Browse</span></span>
- <span data-ttu-id="c2e3f-159">/Store/Details</span><span class="sxs-lookup"><span data-stu-id="c2e3f-159">/Store/Details</span></span>

<span data-ttu-id="c2e3f-160">Bu URL 'Lere erişim, denetleyicimiz içindeki eylem yöntemlerini çağırır ve dize yanıtlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="c2e3f-160">Accessing these URLs will invoke the action methods within our Controller and return string responses:</span></span>

![](mvc-music-store-part-2/_static/image5.png)

<span data-ttu-id="c2e3f-161">Bu harika, ancak bunlar yalnızca sabit dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-161">That's great, but these are just constant strings.</span></span> <span data-ttu-id="c2e3f-162">Böylece, URL 'den bilgi alıp sayfa çıktısında görüntülenecek şekilde dinamik hale olalım.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-162">Let's make them dynamic, so they take information from the URL and display it in the page output.</span></span>

<span data-ttu-id="c2e3f-163">İlk olarak, URL 'den bir QueryString değeri almak için, gezinme eylemi yöntemini değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-163">First we'll change the Browse action method to retrieve a querystring value from the URL.</span></span> <span data-ttu-id="c2e3f-164">Bunu, eylem yönteimize bir "tarz" parametresi ekleyerek yapabiliriz.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-164">We can do this by adding a "genre" parameter to our action method.</span></span> <span data-ttu-id="c2e3f-165">Bu ASP.NET MVC, çağrıldığında otomatik olarak herhangi bir QueryString veya "tarz" adlı form gönderme parametrelerini eylem yönteimize iletir.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-165">When we do this ASP.NET MVC will automatically pass any querystring or form post parameters named "genre" to our action method when it is invoked.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

<span data-ttu-id="c2e3f-166">*Note: Kullanıcı girişini silmek için HttpUtility. HtmlEncode yardımcı programı yöntemini kullanıyoruz. Bu, kullanıcıların JavaScript 'i/Store/gözatmaya benzer bir bağlantıyla ekleme değiştirmesini engeller. Tarz =&lt;betiği&gt;Window. Location = 'http://hackersite.com'&lt;/SCRIPT&gt;.*</span><span class="sxs-lookup"><span data-stu-id="c2e3f-166">*Note: We're using the HttpUtility.HtmlEncode utility method to sanitize the user input. This prevents users from injecting Javascript into our View with a link like /Store/Browse?Genre=&lt;script&gt;window.location='http://hackersite.com'&lt;/script&gt;.*</span></span>

<span data-ttu-id="c2e3f-167">Şimdi/Store/gözatmaya gözatmaya izin veriyor musunuz? Tarz = disco</span><span class="sxs-lookup"><span data-stu-id="c2e3f-167">Now let's browse to /Store/Browse?Genre=Disco</span></span>

![](mvc-music-store-part-2/_static/image6.png)

<span data-ttu-id="c2e3f-168">Daha sonra Ayrıntılar eylemini, ID adlı bir giriş parametresi okumak ve görüntülenecek şekilde değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-168">Let's next change the Details action to read and display an input parameter named ID.</span></span> <span data-ttu-id="c2e3f-169">Önceki yönteminizin aksine ID değerini bir QueryString parametresi olarak gömeceğiz.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-169">Unlike our previous method, we won't be embedding the ID value as a querystring parameter.</span></span> <span data-ttu-id="c2e3f-170">Bunun yerine, bunu doğrudan URL 'nin içine ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-170">Instead we'll embed it directly within the URL itself.</span></span> <span data-ttu-id="c2e3f-171">Örneğin:/Store/Details/5.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-171">For example: /Store/Details/5.</span></span>

<span data-ttu-id="c2e3f-172">ASP.NET MVC bunu, herhangi bir şeyi yapılandırmak zorunda kalmadan kolayca yapabilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-172">ASP.NET MVC lets us easily do this without having to configure anything.</span></span> <span data-ttu-id="c2e3f-173">ASP.NET MVC 'nin varsayılan yönlendirme kuralı, eylem yöntemi adından sonra bir URL 'nin segmentini "ID" adlı bir parametre olarak değerlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-173">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named "ID".</span></span> <span data-ttu-id="c2e3f-174">Eylem yönteminizin ID adlı bir parametresi varsa ASP.NET MVC, URL segmentini otomatik olarak bir parametre olarak size iletir.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-174">If your action method has a parameter named ID then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

<span data-ttu-id="c2e3f-175">Uygulamayı çalıştırın ve/Store/Details/5 adresine gidin:</span><span class="sxs-lookup"><span data-stu-id="c2e3f-175">Run the application and browse to /Store/Details/5:</span></span>

![](mvc-music-store-part-2/_static/image7.png)

<span data-ttu-id="c2e3f-176">Şimdiye kadar yaptığımız şeyleri de en üst sınıra bakalım:</span><span class="sxs-lookup"><span data-stu-id="c2e3f-176">Let's recap what we've done so far:</span></span>

- <span data-ttu-id="c2e3f-177">Visual Web Developer 'da yeni bir ASP.NET MVC projesi oluşturduk</span><span class="sxs-lookup"><span data-stu-id="c2e3f-177">We've created a new ASP.NET MVC project in Visual Web Developer</span></span>
- <span data-ttu-id="c2e3f-178">Bir ASP.NET MVC uygulamasının temel klasör yapısını tartıştık.</span><span class="sxs-lookup"><span data-stu-id="c2e3f-178">We've discussed the basic folder structure of an ASP.NET MVC application</span></span>
- <span data-ttu-id="c2e3f-179">ASP.NET geliştirme sunucusunu kullanarak Web sitemizi nasıl çalıştıracağınızı öğrendiniz</span><span class="sxs-lookup"><span data-stu-id="c2e3f-179">We've learned how to run our website using the ASP.NET Development Server</span></span>
- <span data-ttu-id="c2e3f-180">İki denetleyici sınıfı oluşturduk: bir HomeController ve StoreController</span><span class="sxs-lookup"><span data-stu-id="c2e3f-180">We've created two Controller classes: a HomeController and a StoreController</span></span>
- <span data-ttu-id="c2e3f-181">URL isteklerine yanıt veren ve tarayıcıya metin döndüren denetleyicilerimize eylem yöntemleri ekledik</span><span class="sxs-lookup"><span data-stu-id="c2e3f-181">We've added Action Methods to our controllers which respond to URL requests and return text to the browser</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c2e3f-182">[Önceki](mvc-music-store-part-1.md)
> [İleri](mvc-music-store-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="c2e3f-182">[Previous](mvc-music-store-part-1.md)
[Next](mvc-music-store-part-3.md)</span></span>
