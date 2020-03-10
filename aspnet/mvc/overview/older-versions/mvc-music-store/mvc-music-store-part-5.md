---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: '5\. Bölüm: formları ve şablon oluşturmayı düzenleme | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 5\. bölüm, formları ve şablon oluşturmayı düzenlemenizi içerir.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559551"
---
# <a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="d5769-104">5\. Bölüm: Formları Düzenleme ve Şablon Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5769-104">Part 5: Edit Forms and Templating</span></span>

<span data-ttu-id="d5769-105">[Jon Galloway](https://github.com/jongalloway) tarafından</span><span class="sxs-lookup"><span data-stu-id="d5769-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="d5769-106">MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="d5769-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="d5769-107">MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="d5769-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="d5769-108">Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="d5769-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="d5769-109">5\. bölüm, formları ve şablon oluşturmayı düzenlemenizi içerir.</span><span class="sxs-lookup"><span data-stu-id="d5769-109">Part 5 covers Edit Forms and Templating.</span></span>

<span data-ttu-id="d5769-110">Önceki bölümde, veritabanımızdan veri yüklüyor ve görüntüleme yaptık.</span><span class="sxs-lookup"><span data-stu-id="d5769-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="d5769-111">Bu bölümde, verileri düzenlemenizi de olanaklı yapacağız.</span><span class="sxs-lookup"><span data-stu-id="d5769-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="d5769-112">StoreManagerController oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5769-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="d5769-113">**Storemanagercontroller**adlı yeni bir denetleyici oluşturarak başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="d5769-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="d5769-114">Bu denetleyici için, ASP.NET MVC 3 araçları güncelleştirmesinde bulunan yapı Iskelesi özelliklerinden faydalanacağız.</span><span class="sxs-lookup"><span data-stu-id="d5769-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="d5769-115">Denetleyici Ekle iletişim kutusu seçeneklerini aşağıda gösterildiği gibi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d5769-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="d5769-116">Ekle düğmesine tıkladığınızda, ASP.NET MVC 3 yapı iskelesi mekanizmasının sizin için iyi bir iş miktarı olduğunu görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="d5769-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="d5769-117">Yerel bir Entity Framework değişkeniyle yeni StoreManagerController oluşturur</span><span class="sxs-lookup"><span data-stu-id="d5769-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="d5769-118">Projenin görünümler klasörüne bir StoreManager klasörü ekler</span><span class="sxs-lookup"><span data-stu-id="d5769-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="d5769-119">Bu, albüm sınıfına kesin olarak yazılan Create. cshtml, delete. cshtml, details. cshtml, Edit. cshtml ve Index. cshtml görünümünü ekler</span><span class="sxs-lookup"><span data-stu-id="d5769-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="d5769-120">Yeni StoreManager denetleyici sınıfı, albüm model sınıfıyla çalışmayı ve veritabanı erişimi için Entity Framework bağlamımızı kullanmayı bilen CRUD (oluşturma, okuma, güncelleştirme, silme) denetleyicisi eylemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d5769-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="d5769-121">Bir yapı Iskelesi görünümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="d5769-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="d5769-122">Bu kod, Bu öğreticinin tamamında yazdığımız gibi standart ASP.NET MVC kodsunurken, bu kodun bizim için oluşturulduğunu unutmamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="d5769-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="d5769-123">Ortak denetleyici kodu yazmak ve kesin olarak belirlenmiş görünümleri el ile oluşturmak için harcadığınız zamanı kaydetmek amaçlanmıştır, ancak bu, şu şekilde değişiklik yapma konusunda d uyarılar ile önceden ortaya çıkacak gördüğünüz oluşturulan kod türüdür. kodudur.</span><span class="sxs-lookup"><span data-stu-id="d5769-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="d5769-124">Bu kodunuzda bu sizin değiştirmeniz beklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d5769-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="d5769-125">Bu nedenle, StoreManager dizin görünümüne hızlı bir düzenleme (/views/storemanager/Index.cshtml) ile başlayalım.</span><span class="sxs-lookup"><span data-stu-id="d5769-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="d5769-126">Bu görünüm, depolarımızda düzenleme/Ayrıntılar/silme bağlantılarıyla birlikte gelen albümleri listeleyen bir tablo görüntüler ve albümün ortak özelliklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d5769-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="d5769-127">Bu ekranda çok faydalı olmadığından Albümlerüorturl alanını kaldıracağız.</span><span class="sxs-lookup"><span data-stu-id="d5769-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="d5769-128">Görünüm kodunun &lt;tablo&gt; bölümünde, aşağıdaki vurgulanan satırlarda gösterildiği gibi, albümle birlikte bulunan &lt;&gt; ve &lt;TD öğelerini çevreleyen öğeleri&gt; silin:</span><span class="sxs-lookup"><span data-stu-id="d5769-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="d5769-129">Değiştirilen görünüm kodu şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="d5769-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="d5769-130">Mağaza Yöneticisi 'ne ilk bakış</span><span class="sxs-lookup"><span data-stu-id="d5769-130">A first look at the Store Manager</span></span>

<span data-ttu-id="d5769-131">Şimdi uygulamayı çalıştırın ve/Storemanager/dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="d5769-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="d5769-132">Bu, yeni değiştirdiğimiz mağaza yöneticisi dizinini görüntüleyerek, Düzenle, Ayrıntılar ve Sil bağlantılarıyla depodaki Albümler listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d5769-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="d5769-133">Düzenle bağlantısına tıkladığınızda, albümün alanları içeren bir düzenleme formu görüntülenir ve bu da, tarz ve sanatçının açılan listeleri dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="d5769-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="d5769-134">Alttaki "listeye geri dön" bağlantısına tıklayın ve ardından bir albümün Ayrıntılar bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d5769-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="d5769-135">Bu, tek bir albümün ayrıntı bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d5769-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="d5769-136">Yeniden, listeye geri dön bağlantısına ve ardından silme bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d5769-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="d5769-137">Bu, albüm ayrıntılarını gösteren bir onay iletişim kutusu görüntüler ve bunu silmek istediğdiğimiz emin olup olmadığını sorar.</span><span class="sxs-lookup"><span data-stu-id="d5769-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="d5769-138">Alt kısımdaki Sil düğmesine tıkladığınızda, albüm silinir ve silinen albümün gösterildiği dizin sayfasına dönersiniz.</span><span class="sxs-lookup"><span data-stu-id="d5769-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="d5769-139">Mağaza Yöneticisi ile karşılaştık, ancak başlayacağız CRUD işlemleri için çalışma denetleyicisi ve kod görüntüleme yaptık.</span><span class="sxs-lookup"><span data-stu-id="d5769-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="d5769-140">Mağaza Yöneticisi denetleyici koduna bakıyor</span><span class="sxs-lookup"><span data-stu-id="d5769-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="d5769-141">Mağaza Yöneticisi denetleyicisi iyi bir kod miktarı içerir.</span><span class="sxs-lookup"><span data-stu-id="d5769-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="d5769-142">Bunu yukarıdan aşağıya doğru ilerlim.</span><span class="sxs-lookup"><span data-stu-id="d5769-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="d5769-143">Denetleyici, MVC denetleyicisinin bazı standart ad alanlarını ve modeller ad alanımızın bir başvurusunu içerir.</span><span class="sxs-lookup"><span data-stu-id="d5769-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="d5769-144">Denetleyicinin, veri erişimi için her bir denetleyici eylemi tarafından kullanılan özel bir MusicStoreEntities örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="d5769-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="d5769-145">Mağaza Yöneticisi Dizin ve ayrıntıları eylemleri</span><span class="sxs-lookup"><span data-stu-id="d5769-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="d5769-146">Dizin görünümü, bir albümün başvurulan tarzı ve sanatçı bilgileri de dahil olmak üzere Albümler listesini alır ve daha önce Store Gözatım yönteminde çalışırken gördük.</span><span class="sxs-lookup"><span data-stu-id="d5769-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="d5769-147">Dizin görünümü, bağlantılı nesnelere yapılan başvuruları izleyerek her bir albümün tarz adını ve sanatçı adını görüntüleyebilir, bu nedenle denetleyicinin etkin ve bu bilgileri özgün istekte sorguladığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d5769-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="d5769-148">StoreManager denetleyicisinin Ayrıntılar denetleyicisi eylemi, depolama denetleyicisi ayrıntıları eylemiyle tam olarak aynı şekilde çalışarak Find () yöntemini kullanarak albüm KIMLIĞI için önceden BT sorguları yazdık, sonra da görünüme döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d5769-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="d5769-149">Oluşturma eylemi yöntemleri</span><span class="sxs-lookup"><span data-stu-id="d5769-149">The Create Action Methods</span></span>

<span data-ttu-id="d5769-150">Oluşturma eylemi yöntemleri, şimdiye kadar gördüğdiklerden biraz farklıdır, çünkü form girişi işler.</span><span class="sxs-lookup"><span data-stu-id="d5769-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="d5769-151">Bir Kullanıcı/StoreManager/Create/öğesini ilk kez ziyaret ettiğinde boş bir form görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d5769-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="d5769-152">Bu HTML sayfası, albümün ayrıntılarını girebilecekleri açılan menü ve metin kutusu giriş öğelerini içeren bir &lt;form&gt; öğesi içerir.</span><span class="sxs-lookup"><span data-stu-id="d5769-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="d5769-153">Kullanıcı albüm form değerlerini doldurduktan sonra, bu değişiklikleri veritabanına kaydetmek için bu değişiklikleri uygulamanıza geri göndermek için "Kaydet" düğmesine basabilir.</span><span class="sxs-lookup"><span data-stu-id="d5769-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="d5769-154">Kullanıcı "Kaydet" düğmesine bastığında &lt;form&gt;,/StoreManager/Create/URL 'ye bir HTTP-POST işlemi gerçekleştirir ve &lt;formu&gt; değerlerini HTTP-POST 'un bir parçası olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="d5769-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="d5769-155">ASP.NET MVC, StoreManagerController sınıfımızda iki ayrı "Create" eylem yöntemi uygulamamızı sağlayarak bu iki URL çağırma senaryosunun mantığını kolayca bölmemizi sağlar. ilk HTTP-GET-/StoreManager/Create/URL 'sine gidin ve diğer yandan gönderilen değişikliklerin HTTP-POST işlemini idare edin.</span><span class="sxs-lookup"><span data-stu-id="d5769-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="d5769-156">ViewBag kullanarak bir görünüme bilgi geçirme</span><span class="sxs-lookup"><span data-stu-id="d5769-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="d5769-157">Bu öğreticide daha önce olan görünüm paketini kullandık, ancak bunun çok fazla olmadığı için.</span><span class="sxs-lookup"><span data-stu-id="d5769-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="d5769-158">ViewBag, türü kesin belirlenmiş bir model nesnesi kullanmadan görünüme bilgi iletmemize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5769-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="d5769-159">Bu durumda, HTTP-GET denetleyiciyi Düzenle eyleminin, açılan listeleri doldurmak için forma bir tür ve sanatçı listesi geçirmesi gerekir ve bunu yapmanın en kolay yolu, bunları ViewBag öğeleri olarak döndürmektir.</span><span class="sxs-lookup"><span data-stu-id="d5769-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="d5769-160">ViewBag, bu özellikleri tanımlamak için kod yazmadan ViewBag. foo veya ViewBag. YourNameHere türünde, dinamik bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="d5769-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="d5769-161">Bu durumda, denetleyici kodu ViewBag. Genreıd ve ViewBag. ArtistId ' yi kullanarak, form ile gönderilen aşağı açılan değerlerin Genreıd ve ArtistId olur ve bu da bu ayarların ayartıkları albüm özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="d5769-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="d5769-162">Bu açılan değerler, yalnızca bu amaçla oluşturulan SelectList nesnesi kullanılarak forma döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d5769-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="d5769-163">Bu, aşağıdaki gibi kod kullanılarak yapılır:</span><span class="sxs-lookup"><span data-stu-id="d5769-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="d5769-164">Eylem yöntemi kodundan görebileceğiniz gibi, bu nesneyi oluşturmak için üç parametre kullanılır:</span><span class="sxs-lookup"><span data-stu-id="d5769-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="d5769-165">DropDown 'ın görüntüleneceği öğelerin listesi.</span><span class="sxs-lookup"><span data-stu-id="d5769-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="d5769-166">Bunun yalnızca bir dize olmadığını unutmayın; bir tür listesi geçiriyoruz.</span><span class="sxs-lookup"><span data-stu-id="d5769-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="d5769-167">SelectList öğesine geçirilen sonraki parametre seçili değerdir.</span><span class="sxs-lookup"><span data-stu-id="d5769-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="d5769-168">Bu, SelectList 'in listede bir öğenin nasıl önceden ekleneceğini nasıl öğrendiği.</span><span class="sxs-lookup"><span data-stu-id="d5769-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="d5769-169">Bu, oldukça benzer olan düzenleme formuna baktığımızda anlaşılması daha kolay olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d5769-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="d5769-170">Son parametre, görüntülenecek özelliktir.</span><span class="sxs-lookup"><span data-stu-id="d5769-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="d5769-171">Bu durumda, Genre.Name özelliğinin kullanıcıya gösterildiğine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="d5769-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="d5769-172">Göz önünde bulundurularak, HTTP-GET oluşturma eylemi oldukça basittir; ViewBag 'e iki SelectLists eklenir ve forma hiçbir model nesnesi geçirilmemiştir (henüz oluşturulmadığından).</span><span class="sxs-lookup"><span data-stu-id="d5769-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="d5769-173">Oluştur görünümünde açılan listeleri görüntülemek için HTML Yardımcıları</span><span class="sxs-lookup"><span data-stu-id="d5769-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="d5769-174">Açılan değerlerin görünüme nasıl geçtiğini ele geçirdiğimiz için, bu değerlerin nasıl görüntülendiğini görmek üzere görünüme hızlı bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="d5769-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="d5769-175">Görünüm kodunda (/views/storemanager/Create.exe), tarz açılan ekranını görüntülemek için aşağıdaki çağrının yapıldığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d5769-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="d5769-176">Bu, ortak bir görüntüleme görevi gerçekleştiren bir HTML Yardımcısı-bir yardımcı program yöntemi olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="d5769-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="d5769-177">HTML Yardımcıları, görünüm kodumuzu kısa ve okunabilir halde tutmanın çok yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="d5769-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="d5769-178">HTML. DropDownList Yardımcısı, ASP.NET MVC tarafından sağlanır, ancak daha sonra uygulamamızda yeniden kullanacağımız görünüm kodu için kendi yardımcıları oluşturmak mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d5769-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="d5769-179">HTML. DropDownList çağrısının yalnızca iki şey söyleilmesi gerekir. listenin görüntüleneceği yer, (varsa) bir değer önceden seçilmelidir.</span><span class="sxs-lookup"><span data-stu-id="d5769-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="d5769-180">Birinci parametre olan Genreıd, DropDownList 'e model veya ViewBag içinde Genreıd adlı bir değer bakmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="d5769-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="d5769-181">İkinci parametre, açılan listede başlangıçta seçildiği şekilde gösterilecek değeri göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d5769-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="d5769-182">Bu form bir oluşturma formu olduğundan, önceden seçilecek bir değer yok ve String. Empty geçildi.</span><span class="sxs-lookup"><span data-stu-id="d5769-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="d5769-183">Postalanan form değerlerini işleme</span><span class="sxs-lookup"><span data-stu-id="d5769-183">Handling the Posted Form values</span></span>

<span data-ttu-id="d5769-184">Daha önce anlatıldığı gibi, her formla ilişkili iki eylem yöntemi vardır.</span><span class="sxs-lookup"><span data-stu-id="d5769-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="d5769-185">İlki HTTP-GET isteğini işler ve formu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d5769-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="d5769-186">İkincisi, gönderilen form değerlerini içeren HTTP-POST isteğini işler.</span><span class="sxs-lookup"><span data-stu-id="d5769-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="d5769-187">Denetleyici eyleminin, ASP.NET MVC 'nin yalnızca HTTP-POST isteklerine yanıt vermesi gerektiğini belirten bir [HttpPost] özniteliği olduğunu fark edersiniz.</span><span class="sxs-lookup"><span data-stu-id="d5769-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="d5769-188">Bu eylem dört sorumluluklara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d5769-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="d5769-189">Form değerlerini oku</span><span class="sxs-lookup"><span data-stu-id="d5769-189">Read the form values</span></span>
- 2. <span data-ttu-id="d5769-190">Form değerlerinin herhangi bir doğrulama kuralını geçmediğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="d5769-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="d5769-191">Form gönderimi geçerliyse, verileri kaydedin ve güncelleştirilmiş listeyi görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="d5769-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="d5769-192">Form gönderimi geçerli değilse, doğrulama hatalarıyla formu yeniden görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="d5769-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="d5769-193">Model bağlamasıyla form değerlerini okuma</span><span class="sxs-lookup"><span data-stu-id="d5769-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="d5769-194">Denetleyici eylemi, Genreıd ve ArtistId (açılan listeden) ve başlık, Fiyat ve albümle ilgili metin kutusu değerlerini içeren bir form gönderimini işliyor.</span><span class="sxs-lookup"><span data-stu-id="d5769-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="d5769-195">Form değerlerine doğrudan erişmek mümkün olsa da, ASP.NET MVC içinde yerleşik model bağlama özelliklerini kullanmak daha iyi bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="d5769-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="d5769-196">Bir denetleyici eylemi bir parametre olarak model türü alırsa, ASP.NET MVC Form girişlerini (Ayrıca Route ve QueryString değerlerini) kullanarak o türdeki bir nesneyi doldurmayı dener.</span><span class="sxs-lookup"><span data-stu-id="d5769-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="d5769-197">Bu, adları model nesnesinin özellikleriyle eşleşen değerleri arayarak yapar; örneğin, yeni albüm nesnesinin Genreıd değeri ayarlanırken, Genreıd adında bir giriş arar.</span><span class="sxs-lookup"><span data-stu-id="d5769-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="d5769-198">ASP.NET MVC 'de standart yöntemleri kullanarak görünümler oluşturduğunuzda, formlar her zaman giriş alanı adı olarak özellik adları kullanılarak işlenir, bu nedenle alan adları yalnızca eşleşmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="d5769-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="d5769-199">Model doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="d5769-199">Validating the Model</span></span>

<span data-ttu-id="d5769-200">Model, ModelState. IsValid basit çağrısıyla onaylanır.</span><span class="sxs-lookup"><span data-stu-id="d5769-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="d5769-201">Henüz albüm sınıfınız için herhangi bir doğrulama kuralı eklemediniz. bu şekilde, bu denetim artık bu denetimi çok fazla yapacağız.</span><span class="sxs-lookup"><span data-stu-id="d5769-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="d5769-202">Bu ModelStat. IsValid denetiminin, modelinize yerleştirdiğimiz doğrulama kurallarına uyarlanmasının önemli olması, bu nedenle Doğrulama kurallarındaki gelecekteki değişikliklerin, denetleyici eylem kodunda herhangi bir güncelleştirme gerektirmemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5769-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="d5769-203">Gönderilen değerler kaydediliyor</span><span class="sxs-lookup"><span data-stu-id="d5769-203">Saving the submitted values</span></span>

<span data-ttu-id="d5769-204">Form gönderimi doğrulamayı geçerse, değerleri veritabanına kaydetmeniz zaman olur.</span><span class="sxs-lookup"><span data-stu-id="d5769-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="d5769-205">Entity Framework ile, yalnızca bir modelin Albümler koleksiyonuna eklenmesini ve SaveChanges 'in çağrılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d5769-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="d5769-206">Entity Framework, değeri kalıcı hale getirmek için uygun SQL komutlarını üretir.</span><span class="sxs-lookup"><span data-stu-id="d5769-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="d5769-207">Verileri kaydettikten sonra, güncelleştirmemizi görebilmemiz için Albümler listesine geri yönlendiriyoruz.</span><span class="sxs-lookup"><span data-stu-id="d5769-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="d5769-208">Bu işlem, görüntülenmesini istediğimiz denetleyici eyleminin adı ile RedirectToAction döndürülmesiyle yapılır.</span><span class="sxs-lookup"><span data-stu-id="d5769-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="d5769-209">Bu durumda, Dizin yöntemi budur.</span><span class="sxs-lookup"><span data-stu-id="d5769-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="d5769-210">Doğrulama hatalarıyla geçersiz form gönderimleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="d5769-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="d5769-211">Geçersiz form girişi durumunda, açılan değerler ViewBag 'e eklenir (HTTP-GET durumunda olduğu gibi) ve bağlantılı model değerleri görüntüleme görünümüne geri geçirilir.</span><span class="sxs-lookup"><span data-stu-id="d5769-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="d5769-212">Doğrulama hataları @Html.ValidationMessageFor HTML Yardımcısı kullanılarak otomatik olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d5769-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="d5769-213">Oluşturma formunu test etme</span><span class="sxs-lookup"><span data-stu-id="d5769-213">Testing the Create Form</span></span>

<span data-ttu-id="d5769-214">Bunu test etmek için uygulamayı çalıştırın ve/StoreManager/Create/adresine gidin. Bu, StoreController Create HTTP-GET yöntemi tarafından döndürülen boş formu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d5769-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="d5769-215">Formu göndermek için bazı değerleri girin ve Oluştur düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d5769-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="d5769-216">Düzenlemeleri işleme</span><span class="sxs-lookup"><span data-stu-id="d5769-216">Handling Edits</span></span>

<span data-ttu-id="d5769-217">Düzenleme eylemi çifti (HTTP-GET ve HTTP-POST), az önce bakdığımız oluşturma eylemi yöntemlerine çok benzer.</span><span class="sxs-lookup"><span data-stu-id="d5769-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="d5769-218">Düzenleme senaryosu mevcut bir albümle çalışmayı içerdiğinden, Edit HTTP-GET yöntemi, albümü, yol aracılığıyla geçirilen "ID" parametresine göre yükler.</span><span class="sxs-lookup"><span data-stu-id="d5769-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="d5769-219">Bu kod, Albümno 'a göre bir albümü almaya yönelik bu kod, daha önce ayrıntılar denetleyicisi eyleminde bakdığımız şekilde aynıdır.</span><span class="sxs-lookup"><span data-stu-id="d5769-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="d5769-220">Create/HTTP-GET yönteminde olduğu gibi, açılan değerler de ViewBag aracılığıyla döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d5769-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="d5769-221">Bu, model nesnemiz olarak görünüm (örneğin, bir tarzın listesi) ile ViewBag aracılığıyla bir albüm döndürmemize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5769-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="d5769-222">HTTP-POST işlemini Düzenle eylemi, HTTP-POST oluşturma eylemine çok benzer.</span><span class="sxs-lookup"><span data-stu-id="d5769-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="d5769-223">Tek fark, veritabanına yeni bir albüm eklemek yerine kullanılır. Albümler koleksiyonu, veritabanı kullanarak albümün geçerli örneğini buluyoruz. Giriş (albüm) ve durumunu değiştirildi olarak ayarlama.</span><span class="sxs-lookup"><span data-stu-id="d5769-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="d5769-224">Bu, yeni bir albümü oluşturmak yerine var olan bir albümü değiştirmekte olduğumuz Entity Framework söyler.</span><span class="sxs-lookup"><span data-stu-id="d5769-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="d5769-225">Uygulamayı çalıştırıp/StoreManger/adresine giderek ve ardından bir albümün düzenleme bağlantısına tıklayarak bunu test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5769-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="d5769-226">Bu, düzenleme HTTP-GET yöntemi tarafından gösterilen düzenleme formunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d5769-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="d5769-227">Bazı değerleri girin ve Kaydet düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d5769-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="d5769-228">Bu, formu gönderir, değerleri kaydeder ve ABD 'nin güncelleştirildiğini gösteren albüm listesine döndürür.</span><span class="sxs-lookup"><span data-stu-id="d5769-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="d5769-229">Silme Işlemi işleniyor</span><span class="sxs-lookup"><span data-stu-id="d5769-229">Handling Deletion</span></span>

<span data-ttu-id="d5769-230">Silme, düzenleme ve oluşturma ile aynı kalıbı izler, onay formunu göstermek için bir denetleyici eylemi ve form gönderimini işlemek için başka bir denetleyici eylemi kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="d5769-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="d5769-231">HTTP-GET Delete Controller eylemi, önceki Store Manager ayrıntıları denetleyicisi eylemmizden tamamen aynıdır.</span><span class="sxs-lookup"><span data-stu-id="d5769-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="d5769-232">Görünüm içeriğini sil şablonunu kullanarak bir albüm türüne kesin olarak yazılmış bir form görüntüyoruz.</span><span class="sxs-lookup"><span data-stu-id="d5769-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="d5769-233">Şablonu Sil, modelin tüm alanlarını gösterir, ancak bu şekilde bir bit ' i basitleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="d5769-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="d5769-234">/Views/storemanager/delete.exe ' deki görünüm kodunu aşağıdaki şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d5769-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="d5769-235">Bu, Basitleştirilmiş bir silme onayı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d5769-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="d5769-236">Sil düğmesine tıkladığınızda formun sunucuya geri nakledilmesine neden olur ve bu da Deleteonaylanan eylemi yürütür.</span><span class="sxs-lookup"><span data-stu-id="d5769-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="d5769-237">HTTP-POST silme denetleyici eylemi aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="d5769-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="d5769-238">Albümü KIMLIĞE göre yükler</span><span class="sxs-lookup"><span data-stu-id="d5769-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="d5769-239">Albümü siler ve değişiklikleri kaydeder</span><span class="sxs-lookup"><span data-stu-id="d5769-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="d5769-240">Albümün listeden kaldırıldığını gösteren dizine yeniden yönlendirir</span><span class="sxs-lookup"><span data-stu-id="d5769-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="d5769-241">Bunu test etmek için uygulamayı çalıştırın ve/Storemanagera gidin.</span><span class="sxs-lookup"><span data-stu-id="d5769-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="d5769-242">Listeden bir albüm seçin ve Sil bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d5769-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="d5769-243">Bu, silme onayı ekranımızı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d5769-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="d5769-244">Sil düğmesine tıkladığınızda albüm kaldırılır ve bu, albümün silindiğini gösteren mağaza yöneticisi dizin sayfasına döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d5769-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="d5769-245">Metni kesmek için özel HTML Yardımcısı kullanma</span><span class="sxs-lookup"><span data-stu-id="d5769-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="d5769-246">Store Manager Dizin sayfamızda bir olası sorun var.</span><span class="sxs-lookup"><span data-stu-id="d5769-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="d5769-247">Albüm başlığımız ve sanatçı adı özellikleri, tablo biçimimizi oluşturabilecek kadar uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="d5769-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="d5769-248">Görünümlerimizde bu ve diğer özellikleri kolayca kesmemizi sağlamak için özel bir HTML Yardımcısı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="d5769-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="d5769-249">Razor @helper söz dizimi, görünümlerinizin kullanımı için kendi yardımcı işlevlerinizi oluşturmayı oldukça kolay hale yaptı.</span><span class="sxs-lookup"><span data-stu-id="d5769-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="d5769-250">/Views/storemanager/Index.cshtml görünümünü açın ve @model satırından hemen sonra aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d5769-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="d5769-251">Bu yardımcı yöntem, izin vermek için bir dize ve en fazla uzunluğu alır.</span><span class="sxs-lookup"><span data-stu-id="d5769-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="d5769-252">Sağlanan metin belirtilen uzunluktan kısaysa, yardımcı bunu olduğu gibi verir.</span><span class="sxs-lookup"><span data-stu-id="d5769-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="d5769-253">Daha uzunsa, metni keser ve "..." oluşturur geri kalanı için.</span><span class="sxs-lookup"><span data-stu-id="d5769-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="d5769-254">Şimdi, albüm başlığı ve sanatçı adı özelliklerinin 25 karakterden az olduğundan emin olmak için Truncate Helper 'ı kullanabiliriz.</span><span class="sxs-lookup"><span data-stu-id="d5769-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="d5769-255">Yeni kesme yardımımızın kullanıldığı tüm görünüm kodu aşağıda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d5769-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="d5769-256">Şimdi/StoreManager/URL 'ye gözatarken, albümler ve başlıklar en büyük uzunlularımızın altında tutulur.</span><span class="sxs-lookup"><span data-stu-id="d5769-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="d5769-257">Note: Bu, bir yardım 'ın tek bir görünümde oluşturulması ve kullanılması için basit bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="d5769-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="d5769-258">Siteniz genelinde kullanabileceğiniz yardımcılar oluşturma hakkında daha fazla bilgi edinmek için bkz. blog gönderisi: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span><span class="sxs-lookup"><span data-stu-id="d5769-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d5769-259">[Önceki](mvc-music-store-part-4.md)
> [İleri](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="d5769-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>
