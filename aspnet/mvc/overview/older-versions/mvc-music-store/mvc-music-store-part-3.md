---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: '3\. kısım: görünümler ve Viewmodeller | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 3, görünümleri ve ViewModel içerir.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559810"
---
# <a name="part-3-views-and-viewmodels"></a><span data-ttu-id="3ea73-104">3\. Bölüm: Görünümler ve ViewModel’lar</span><span class="sxs-lookup"><span data-stu-id="3ea73-104">Part 3: Views and ViewModels</span></span>

<span data-ttu-id="3ea73-105">[Jon Galloway](https://github.com/jongalloway) tarafından</span><span class="sxs-lookup"><span data-stu-id="3ea73-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="3ea73-106">MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="3ea73-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="3ea73-107">MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="3ea73-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="3ea73-108">Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="3ea73-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="3ea73-109">Bölüm 3, görünümleri ve ViewModel içerir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-109">Part 3 covers Views and ViewModels.</span></span>

<span data-ttu-id="3ea73-110">Şu ana kadar yalnızca denetleyici eylemlerinden dizeler döndürdük.</span><span class="sxs-lookup"><span data-stu-id="3ea73-110">So far we've just been returning strings from controller actions.</span></span> <span data-ttu-id="3ea73-111">Bu, denetleyicilerin nasıl çalıştığı konusunda fikir sahibi olmak için iyi bir yoldur, ancak gerçek bir Web uygulaması oluşturmak istemekten değildir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-111">That's a nice way to get an idea of how controllers work, but it's not how you'd want to build a real web application.</span></span> <span data-ttu-id="3ea73-112">Sitemizi ziyaret eden tarayıcılarımıza geri HTML oluşturmak için daha iyi bir yol isteyeceksiniz. Bu, şablon dosyalarını yalnızca bir HTML içeriğini geri gönder ' i daha kolay özelleştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-112">We are going to want a better way to generate HTML back to browsers visiting our site – one where we can use template files to more easily customize the HTML content send back.</span></span> <span data-ttu-id="3ea73-113">Tam olarak bu görünümler vardır.</span><span class="sxs-lookup"><span data-stu-id="3ea73-113">That's exactly what Views do.</span></span>

## <a name="adding-a-view-template"></a><span data-ttu-id="3ea73-114">Görünüm şablonu ekleme</span><span class="sxs-lookup"><span data-stu-id="3ea73-114">Adding a View template</span></span>

<span data-ttu-id="3ea73-115">Bir görünüm şablonu kullanmak için, HomeController Dizin yöntemini bir ActionResult döndürecek şekilde değiştirecek ve aşağıdaki gibi bir görünüm () döndürüyor.</span><span class="sxs-lookup"><span data-stu-id="3ea73-115">To use a view-template, we'll change the HomeController Index method to return an ActionResult, and have it return View(), like below:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

<span data-ttu-id="3ea73-116">Yukarıdaki değişiklik, bir dize döndürmesinin yerine, bir sonuç oluşturmak için bir "Görünüm" kullanmak istediğinin olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-116">The above change indicates that instead of returned a string, we instead want to use a "View" to generate a result back.</span></span>

<span data-ttu-id="3ea73-117">Şimdi projemizi uygun bir görünüm şablonu ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-117">We'll now add an appropriate View template to our project.</span></span> <span data-ttu-id="3ea73-118">Bunu yapmak için, metin imlecini Dizin eylemi yöntemine konumlandırır, sonra sağ tıklayıp "Görünüm Ekle" seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="3ea73-118">To do this we'll position the text cursor within the Index action method, then right-click and select "Add View".</span></span> <span data-ttu-id="3ea73-119">Bu işlem, Görünüm Ekle iletişim kutusunu getirir:</span><span class="sxs-lookup"><span data-stu-id="3ea73-119">This will bring up the Add View dialog:</span></span>

<span data-ttu-id="3ea73-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3ea73-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span></span>

<span data-ttu-id="3ea73-121">"Görünüm Ekle" iletişim kutusu, görünüm şablonu dosyalarını hızlı ve kolay bir şekilde üretmemize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ea73-121">The "Add View" dialog allows us to quickly and easily generate View template files.</span></span> <span data-ttu-id="3ea73-122">Varsayılan olarak, "Görünüm Ekle" iletişim kutusu, oluşturulacak eylem yöntemiyle eşleşecek şekilde oluşturmak için görünüm şablonunun adını önceden doldurur.</span><span class="sxs-lookup"><span data-stu-id="3ea73-122">By default the "Add View" dialog pre-populates the name of the View template to create so that it matches the action method that will use it.</span></span> <span data-ttu-id="3ea73-123">HomeController 'ın Index () eylem yöntemi içinde "Görünüm Ekle" bağlam menüsünü kullandığımız için, yukarıdaki "Görünüm Ekle" iletişim kutusunda varsayılan olarak önceden doldurulan görünüm adı olarak "Dizin" bulunur.</span><span class="sxs-lookup"><span data-stu-id="3ea73-123">Because we used the "Add View" context menu within the Index() action method of our HomeController, the "Add View" dialog above has "Index" as the view name pre-populated by default.</span></span> <span data-ttu-id="3ea73-124">Bu iletişim kutusundaki seçeneklerden herhangi birini değiştirmemiz gerekmez, bu nedenle Ekle düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3ea73-124">We don't need to change any of the options on this dialog, so click the Add button.</span></span>

<span data-ttu-id="3ea73-125">Ekle düğmesine tıkladığımızda, Visual Web Developer, daha önce yoksa klasörü oluşturmak için \Views\Home dizininde yeni bir Index. cshtml görünüm şablonu oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="3ea73-125">When we click the Add button, Visual Web Developer will create a new Index.cshtml view template for us in the \Views\Home directory, creating the folder if doesn't already exist.</span></span>

![](mvc-music-store-part-3/_static/image2.png)

<span data-ttu-id="3ea73-126">"Index. cshtml" dosyasının adı ve klasör konumu önemlidir ve varsayılan ASP.NET MVC adlandırma kurallarını izler.</span><span class="sxs-lookup"><span data-stu-id="3ea73-126">The name and folder location of the "Index.cshtml" file is important, and follows the default ASP.NET MVC naming conventions.</span></span> <span data-ttu-id="3ea73-127">\Views\Home dizin adı, HomeController adlı denetleyiciyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-127">The directory name, \Views\Home, matches the controller - which is named HomeController.</span></span> <span data-ttu-id="3ea73-128">Görünüm şablonu adı, dizin, görünümü görüntüleyen denetleyici eylemi yöntemiyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-128">The view template name, Index, matches the controller action method which will be displaying the view.</span></span>

<span data-ttu-id="3ea73-129">ASP.NET MVC, bir görünüm döndürmek için bu adlandırma kuralını kullanırken bir görünüm şablonunun adını veya konumunu açık bir şekilde belirtmemizi önlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="3ea73-129">ASP.NET MVC allows us to avoid having to explicitly specify the name or location of a view template when we use this naming convention to return a view.</span></span> <span data-ttu-id="3ea73-130">Bu, varsayılan olarak \Views\home\ındex.cshtml görünüm şablonunu izleyerek HomeController içinde aşağıdaki gibi kod yazdığımızda işlenir:</span><span class="sxs-lookup"><span data-stu-id="3ea73-130">It will by default render the \Views\Home\Index.cshtml view template when we write code like below within our HomeController:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

<span data-ttu-id="3ea73-131">"Görünüm Ekle" iletişim kutusunda "Ekle" düğmesine tıkladıktan sonra Visual Web Developer "Index. cshtml" görünüm şablonunu oluşturup açtı.</span><span class="sxs-lookup"><span data-stu-id="3ea73-131">Visual Web Developer created and opened the "Index.cshtml" view template after we clicked the "Add" button within the "Add View" dialog.</span></span> <span data-ttu-id="3ea73-132">Index. cshtml 'nin içerikleri aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-132">The contents of Index.cshtml are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

<span data-ttu-id="3ea73-133">Bu görünüm, ASP.NET Web Forms ve önceki ASP.NET MVC sürümlerinde kullanılan Web Forms görünüm altyapısından daha kısa olan Razor söz dizimi kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="3ea73-133">This view is using the Razor syntax, which is more concise than the Web Forms view engine used in ASP.NET Web Forms and previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="3ea73-134">Web Forms View Engine, ASP.NET MVC 3 ' te hala kullanılabilir, ancak birçok geliştirici Razor görünüm altyapısının ASP.NET MVC geliştirme sürecinde uygun olduğunu bulur.</span><span class="sxs-lookup"><span data-stu-id="3ea73-134">The Web Forms view engine is still available in ASP.NET MVC 3, but many developers find that the Razor view engine fits ASP.NET MVC development really well.</span></span>

<span data-ttu-id="3ea73-135">İlk üç satır, ViewBag. title kullanarak sayfa başlığını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3ea73-135">The first three lines set the page title using ViewBag.Title.</span></span> <span data-ttu-id="3ea73-136">Bunun kısa süre içinde nasıl çalıştığını inceleyeceğiz, ancak ilk olarak metin başlık metnini güncelleştirip sayfayı görüntüleyelim.</span><span class="sxs-lookup"><span data-stu-id="3ea73-136">We'll look at how this works in more detail soon, but first let's update the text heading text and view the page.</span></span> <span data-ttu-id="3ea73-137">&lt;H2&gt; etiketini aşağıda gösterildiği gibi "Bu giriş sayfasıdır" olarak güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3ea73-137">Update the &lt;h2&gt; tag to say "This is the Home Page" as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

<span data-ttu-id="3ea73-138">Uygulamanın çalıştırılması, yeni metnimizin giriş sayfasında görünür olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-138">Running the application shows that our new text is visible on the home page.</span></span>

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a><span data-ttu-id="3ea73-139">Ortak site öğeleri için Düzen kullanma</span><span class="sxs-lookup"><span data-stu-id="3ea73-139">Using a Layout for common site elements</span></span>

<span data-ttu-id="3ea73-140">Çoğu Web sitesinin birçok sayfa arasında paylaşılan içeriği vardır: gezinme, altbilgiler, logo görüntüleri, stil sayfası başvuruları, vb. Razor Görünüm altyapısı, bu işlemi otomatik olarak/Views/Shared klasöründe oluşturulan \_Layout. cshtml adlı bir sayfa kullanarak yönetmeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="3ea73-140">Most websites have content which is shared between many pages: navigation, footers, logo images, stylesheet references, etc. The Razor view engine makes this easy to manage using a page called \_Layout.cshtml which has automatically been created for us inside the /Views/Shared folder.</span></span>

![](mvc-music-store-part-3/_static/image4.png)

<span data-ttu-id="3ea73-141">Aşağıda gösterilen içerikleri görüntülemek için bu klasöre çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3ea73-141">Double-click on this folder to view the contents, which are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

<span data-ttu-id="3ea73-142">Bireysel görünümlerimizin içeriği, @RenderBody() komutuyla ve bunun dışında görünmesini istediğimiz tüm ortak içerikler, \_Layout. cshtml biçimlendirmesine eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-142">The content from our individual views will be displayed by the @RenderBody() command, and any common content that we want to appear outside of that can be added to the \_Layout.cshtml markup.</span></span> <span data-ttu-id="3ea73-143">MVC müzik mağazamız, sitedeki tüm sayfalarda giriş sayfası ve depolama alanı bağlantılarıyla ortak bir üst bilgiye sahip olmasını istiyoruz, bu nedenle bu @RenderBody() deyimin hemen üstüne bu şablonu ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-143">We'll want our MVC Music Store to have a common header with links to our Home page and Store area on all pages in the site, so we'll add that to the template directly above that @RenderBody() statement.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a><span data-ttu-id="3ea73-144">Stil sayfasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="3ea73-144">Updating the StyleSheet</span></span>

<span data-ttu-id="3ea73-145">Boş proje şablonu, yalnızca doğrulama iletilerini göstermek için kullanılan stilleri içeren çok kolaylaştırılmış bir CSS dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-145">The empty project template includes a very streamlined CSS file which just includes styles used to display validation messages.</span></span> <span data-ttu-id="3ea73-146">Tasarımcı, sitemizin görünümünü tanımlamak için bazı ek CSS ve görüntüler sağladı, bu nedenle bunları şimdi ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-146">Our designer has provided some additional CSS and images to define the look and feel for our site, so we'll add those in now.</span></span>

<span data-ttu-id="3ea73-147">Güncelleştirilmiş CSS dosyası ve görüntüleri, [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store)' da bulunan MvcMusicStore-assets. zip ' in içerik dizinine dahildir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-147">The updated CSS file and Images are included in the Content directory of MvcMusicStore-Assets.zip which is available at [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span> <span data-ttu-id="3ea73-148">Bunları Windows Gezgini 'nde her ikisini de seçeceğiz ve Visual Web Developer 'daki çözümünüzün Içerik klasörüne aşağıda gösterildiği gibi bırakmalısınız:</span><span class="sxs-lookup"><span data-stu-id="3ea73-148">We'll select both of them in Windows Explorer and drop them into our Solution's Content folder in Visual Web Developer, as shown below:</span></span>

![](mvc-music-store-part-3/_static/image5.png)

<span data-ttu-id="3ea73-149">Mevcut site. css dosyasının üzerine yazmak isteyip istemediğinizi onaylamanız istenecektir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-149">You'll be asked to confirm if you want to overwrite the existing Site.css file.</span></span> <span data-ttu-id="3ea73-150">Evet’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3ea73-150">Click Yes.</span></span>

![](mvc-music-store-part-3/_static/image6.png)

<span data-ttu-id="3ea73-151">Uygulamanızın Içerik klasörü şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="3ea73-151">The Content folder of your application will now appear as follows:</span></span>

![](mvc-music-store-part-3/_static/image7.png)

<span data-ttu-id="3ea73-152">Şimdi uygulamayı çalıştıralım ve değişikliklerin giriş sayfasında nasıl görünemizi görelim.</span><span class="sxs-lookup"><span data-stu-id="3ea73-152">Now let's run the application and see how our changes look on the Home page.</span></span>

![](mvc-music-store-part-3/_static/image8.png)

- <span data-ttu-id="3ea73-153">Nelerin değiştiğini gözden geçirelim: HomeController 'ın Dizin eylemi yöntemi, "Return View ()" olarak adlandırılsa da, "dönüş görünümü ()" olarak adlandırılsa da, "döndürülen görünüm ()" olarak adlandırılsa da, izleme şablonunuz standart adlandırma kuralına uyduğundan, \ views\home\ındex</span><span class="sxs-lookup"><span data-stu-id="3ea73-153">Let's review what's changed: The HomeController's Index action method found and displayed the \Views\Home\Index.cshtmlView template, even though our code called "return View()", because our View template followed the standard naming convention.</span></span>
- <span data-ttu-id="3ea73-154">Giriş sayfası, \Views\home\ındex.cshtml görünüm şablonu içinde tanımlanan basit bir hoş geldiniz iletisi görüntülüyor.</span><span class="sxs-lookup"><span data-stu-id="3ea73-154">The Home Page is displaying a simple welcome message that is defined within the \Views\Home\Index.cshtml view template.</span></span>
- <span data-ttu-id="3ea73-155">Giriş sayfası \_Layout. cshtml şablonumuzu kullanıyor ve bu nedenle hoş geldiniz iletisi standart site HTML düzeni içinde yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="3ea73-155">The Home Page is using our \_Layout.cshtml template, and so the welcome message is contained within the standard site HTML layout.</span></span>

## <a name="using-a-model-to-pass-information-to-our-view"></a><span data-ttu-id="3ea73-156">Görünümümüze bilgi geçirmek için bir model kullanma</span><span class="sxs-lookup"><span data-stu-id="3ea73-156">Using a Model to pass information to our View</span></span>

<span data-ttu-id="3ea73-157">Yalnızca sabit kodlanmış HTML 'yi görüntüleyen bir görünüm şablonu, çok ilgi çekici bir Web sitesi yapamıyor.</span><span class="sxs-lookup"><span data-stu-id="3ea73-157">A View template that just displays hardcoded HTML isn't going to make a very interesting web site.</span></span> <span data-ttu-id="3ea73-158">Dinamik bir Web sitesi oluşturmak için, denetleyici eylemlerimizden görünüm Şablonlarımıza bilgi geçirmek istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-158">To create a dynamic web site, we'll instead want to pass information from our controller actions to our view templates.</span></span>

<span data-ttu-id="3ea73-159">Model-View-Controller düzeninde model terimi, uygulamadaki verileri temsil eden nesneleri ifade eder.</span><span class="sxs-lookup"><span data-stu-id="3ea73-159">In the Model-View-Controller pattern, the term Model refers to objects which represent the data in the application.</span></span> <span data-ttu-id="3ea73-160">Genellikle, model nesneleri veritabanınızdaki tablolara karşılık gelir, ancak bunlara gerek kalmaz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-160">Often, model objects correspond to tables in your database, but they don't have to.</span></span>

<span data-ttu-id="3ea73-161">Bir ActionResult döndüren denetleyici eylemi metotları bir model nesnesini görünüme geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-161">Controller action methods which return an ActionResult can pass a model object to the view.</span></span> <span data-ttu-id="3ea73-162">Bu, bir denetleyicinin yanıt oluşturmak için gereken tüm bilgileri düzgün bir şekilde paketleyip bu bilgileri uygun HTML yanıtını oluşturmak için kullanılacak bir görünüm şablonuna iletmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ea73-162">This allows a Controller to cleanly package up all the information needed to generate a response, and then pass this information off to a View template to use to generate the appropriate HTML response.</span></span> <span data-ttu-id="3ea73-163">Bu işlemin anlaşılması en kolay yöntemdir. bu nedenle kullanmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="3ea73-163">This is easiest to understand by seeing it in action, so let's get started.</span></span>

<span data-ttu-id="3ea73-164">İlk olarak, mağazamız içindeki tarzları ve albümleri temsil eden bazı model sınıfları oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="3ea73-164">First we'll create some Model classes to represent Genres and Albums within our store.</span></span> <span data-ttu-id="3ea73-165">Bir tarz sınıfı oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="3ea73-165">Let's start by creating a Genre class.</span></span> <span data-ttu-id="3ea73-166">Projenizin içindeki "modeller" klasörüne sağ tıklayın, "Sınıf Ekle" seçeneğini belirleyin ve "Genre.cs" dosyasını adlandırın.</span><span class="sxs-lookup"><span data-stu-id="3ea73-166">Right-click the "Models" folder within your project, choose the "Add Class" option, and name the file "Genre.cs".</span></span>

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

<span data-ttu-id="3ea73-167">Ardından oluşturulan sınıfa ortak bir dize adı özelliği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3ea73-167">Then add a public string Name property to the class that was created:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

<span data-ttu-id="3ea73-168">*Note: merak ediyorsanız, {get; set;} gösterimi, otomatik olarak C#uygulanan özellikler özelliğinin kullanımını yapıyor. Bu, bir destek alanı bildirmek zorunda kalmadan bir özelliğin avantajlarından yararlanmanızı sağlar.*</span><span class="sxs-lookup"><span data-stu-id="3ea73-168">*Note: In case you're wondering, the { get; set; } notation is making use of C#'s auto-implemented properties feature. This gives us the benefits of a property without requiring us to declare a backing field.*</span></span>

<span data-ttu-id="3ea73-169">Ardından, bir başlık ve bir tarz özelliği olan bir albüm sınıfı (Album.cs adlı) oluşturmak için aynı adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="3ea73-169">Next, follow the same steps to create an Album class (named Album.cs) that has a Title and a Genre property:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

<span data-ttu-id="3ea73-170">Artık, modelinizdeki dinamik bilgileri görüntüleyen görünümleri kullanmak için StoreController 'ı değiştirebiliriz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-170">Now we can modify the StoreController to use Views which display dynamic information from our Model.</span></span> <span data-ttu-id="3ea73-171">Daha önce tanıtım amaçlı olarak, istek KIMLIĞINE göre albümlerimizi adlandırdık, bu bilgileri aşağıdaki görünümde olduğu gibi görüntüleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-171">If - for demonstration purposes right now - we named our Albums based on the request ID, we could display that information as in the view below.</span></span>

![](mvc-music-store-part-3/_static/image10.png)

<span data-ttu-id="3ea73-172">Mağaza ayrıntıları eylemini değiştirerek başlayacağız, bu nedenle tek bir albümün bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-172">We'll start by changing the Store Details action so it shows the information for a single album.</span></span> <span data-ttu-id="3ea73-173">MvcMusicStore. model ad alanını dahil etmek için **Storecontrollers** sınıfının en üstüne bir "Using" ifadesini ekleyin. bu nedenle, albüm sınıfını kullanmak istediğimiz her seferinde MvcMusicStore. modeller. albümünü yazmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3ea73-173">Add a "using" statement to the top of the **StoreControllers** class to include the MvcMusicStore.Models namespace, so we don't need to type MvcMusicStore.Models.Album every time we want to use the album class.</span></span> <span data-ttu-id="3ea73-174">Bu sınıfın "kullanımlar" bölümü şimdi aşağıda gösterildiği gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-174">The "usings" section of that class should now appear as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

<span data-ttu-id="3ea73-175">Daha sonra, HomeController 'ın Dizin yöntemiyle yaptığımız gibi, bir dize yerine bir ActionResult döndüren Ayrıntılar denetleyicisi eylemini güncelleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-175">Next, we'll update the Details controller action so that it returns an ActionResult rather than a string, as we did with the HomeController's Index method.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

<span data-ttu-id="3ea73-176">Şimdi görünüme bir albüm nesnesi döndürecek mantığı değiştirebiliriz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-176">Now we can modify the logic to return an Album object to the view.</span></span> <span data-ttu-id="3ea73-177">Bu öğreticide daha sonra verileri bir veritabanından alacak, ancak şu anda başlamak için "kukla verileri" kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="3ea73-177">Later in this tutorial we will be retrieving the data from a database – but for right now we will use "dummy data" to get started.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

<span data-ttu-id="3ea73-178">*Note: hakkında bilginiz varsa C#, bunu kullanarak, albüm değişkenimizin geç bağlantılı olduğu anlamına gelebilir. Bu doğru değildir: C# derleyici, albümün albüm türünde olduğunu belirlemek ve yerel albüm değişkenini bir albüm türü olarak derlemek için değişkene neleri atadığımızda tür çıkarımı kullanıyor, bu nedenle derleme zamanı denetimi ve Visual Studio kod Düzenleyicisi desteği sunuyoruz.*</span><span class="sxs-lookup"><span data-stu-id="3ea73-178">*Note: If you're unfamiliar with C#, you may assume that using var means that our album variable is late-bound. That's not correct – the C# compiler is using type-inference based on what we're assigning to the variable to determine that album is of type Album and compiling the local album variable as an Album type, so we get compile-time checking and Visual Studio code-editor support.*</span></span>

<span data-ttu-id="3ea73-179">Şimdi de HTML yanıtı oluşturmak için albümümüzü kullanan bir görünüm şablonu oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="3ea73-179">Let's now create a View template that uses our Album to generate an HTML response.</span></span> <span data-ttu-id="3ea73-180">Bunu yapmadan önce, görünümü Ekle iletişim kutusu yeni oluşturulan albüm sınıfınızı hakkında bilgi sahibi olacak şekilde projeyi derliyoruz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-180">Before we do that we need to build the project so that the Add View dialog knows about our newly created Album class.</span></span> <span data-ttu-id="3ea73-181">Projeyi, hata ayıkla ⇨ Build MvcMusicStore menü öğesini seçerek oluşturabilirsiniz (ek kredi için, projeyi derlemek için Ctrl-Shift-B kısayolunu kullanabilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="3ea73-181">You can build the project by selecting the Debug⇨Build MvcMusicStore menu item (for extra credit, you can use the Ctrl-Shift-B shortcut to build the project).</span></span>

![](mvc-music-store-part-3/_static/image11.png)

<span data-ttu-id="3ea73-182">Artık destekleyici sınıflarınızı ayarladığımıza göre, görünüm şablonumuzu oluşturmaya hazır olduğumuz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-182">Now that we've set up our supporting classes, we're ready to build our View template.</span></span> <span data-ttu-id="3ea73-183">Ayrıntılar yöntemine sağ tıklayın ve "Görünüm Ekle..." öğesini seçin. bağlam menüsünden.</span><span class="sxs-lookup"><span data-stu-id="3ea73-183">Right-click within the Details method and select "Add View…" from the context menu.</span></span>

![](mvc-music-store-part-3/_static/image12.png)

<span data-ttu-id="3ea73-184">HomeController 'tan önce yaptığımız gibi yeni bir görünüm şablonu oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="3ea73-184">We are going to create a new View template like we did before with the HomeController.</span></span> <span data-ttu-id="3ea73-185">Bunu StoreController 'dan oluşturduğumuz için varsayılan olarak \Views\store\ındex.cshtml dosyasında oluşturulacaktır.</span><span class="sxs-lookup"><span data-stu-id="3ea73-185">Because we are creating it from the StoreController it will by default be generated in a \Views\Store\Index.cshtml file.</span></span>

<span data-ttu-id="3ea73-186">Daha önce olduğu gibi, "kesin olarak belirlenmiş bir" görünümü oluşturma onay kutusunu denetleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-186">Unlike before, we are going to check the "Create a strongly-typed" view checkbox.</span></span> <span data-ttu-id="3ea73-187">Daha sonra "veri sınıfı görüntüle" aşağı açılan listesinde "albüm" sınıfınızı seçeceğiz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-187">We are then going to select our "Album" class within the "View data-class" drop-downlist.</span></span> <span data-ttu-id="3ea73-188">Bu, "Görünüm Ekle" iletişim kutusunun bir albüm nesnesinin kullanmak üzere geçirilmesini bekleyen bir görünüm şablonu oluşturmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="3ea73-188">This will cause the "Add View" dialog to create a View template that expects that an Album object will be passed to it to use.</span></span>

![](mvc-music-store-part-3/_static/image13.png)

<span data-ttu-id="3ea73-189">\Views\Store\Details.cshtml görünüm şablonumuz "Ekle" düğmesine tıkladığımızda, aşağıdaki kodu içeren oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="3ea73-189">When we click the "Add" button our \Views\Store\Details.cshtml View template will be created, containing the following code.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

<span data-ttu-id="3ea73-190">Bu görünümün, albüm sınıfımızda kesin olarak yazılmış olduğunu gösteren ilk satıra dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="3ea73-190">Notice the first line, which indicates that this view is strongly-typed to our Album class.</span></span> <span data-ttu-id="3ea73-191">Razor görünümü altyapısı, bir albüm nesnesi geçtiğini anladığından, model özelliklerine kolayca erişebilmemiz ve hatta Visual Web Developer Editor 'da IntelliSense 'in avantajlarından yararlanabiliyoruz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-191">The Razor view engine understands that it has been passed an Album object, so we can easily access model properties and even have the benefit of IntelliSense in the Visual Web Developer editor.</span></span>

<span data-ttu-id="3ea73-192">&lt;H2&gt; etiketini, bu satırı aşağıdaki gibi görünecek şekilde değiştirerek albümün title özelliğini görüntüleyecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3ea73-192">Update the &lt;h2&gt; tag so it displays the Album's Title property by modifying that line to appear as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

<span data-ttu-id="3ea73-193">@Model anahtar sözcüğünden sonra, albüm sınıfının desteklediği özellikleri ve yöntemleri göstererek, IntelliSense 'in tetiklendiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="3ea73-193">Notice that IntelliSense is triggered when you enter the period after the @Model keyword, showing the properties and methods that the Album class supports.</span></span>

<span data-ttu-id="3ea73-194">Şimdi projemizi yeniden çalıştırıp/Store/Details/5 URL 'sini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="3ea73-194">Let's now re-run our project and visit the /Store/Details/5 URL.</span></span> <span data-ttu-id="3ea73-195">Aşağıdaki gibi bir albümün ayrıntılarını görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-195">We'll see details of an Album like below.</span></span>

![](mvc-music-store-part-3/_static/image14.png)

<span data-ttu-id="3ea73-196">Şimdi mağaza tarama eylemi yöntemine benzer bir güncelleştirme yapacağız.</span><span class="sxs-lookup"><span data-stu-id="3ea73-196">Now we'll make a similar update for the Store Browse action method.</span></span> <span data-ttu-id="3ea73-197">Yöntemi bir ActionResult döndüren şekilde güncelleştirin ve yöntem mantığını yeni bir tarz nesnesi oluşturacak ve görünüme döndüren şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3ea73-197">Update the method so it returns an ActionResult, and modify the method logic so it creates a new Genre object and returns it to the View.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

<span data-ttu-id="3ea73-198">Tarayıcı yöntemine sağ tıklayın ve "Görünüm Ekle..." seçeneğini belirleyin. bağlam menüsünden, türü kesin belirlenmiş bir görünüm ekleyin ve tarz sınıfına kesin bir tür ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3ea73-198">Right-click in the Browse method and select "Add View…" from the context menu, then add a View that is strongly-typed add a strongly typed to the Genre class.</span></span>

![](mvc-music-store-part-3/_static/image15.png)

<span data-ttu-id="3ea73-199">Görünüm kodundaki &lt;H2&gt; öğesini (/Views/Store/Browse.cshtml 'de), tarz bilgilerini görüntülemek için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3ea73-199">Update the &lt;h2&gt; element in the view code (in /Views/Store/Browse.cshtml) to display the Genre information.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

<span data-ttu-id="3ea73-200">Şimdi, projemizi yeniden çalıştırıp/Store/zat mı gözatalim? Tarz = disco URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="3ea73-200">Now let's re-run our project and browse to the /Store/Browse?Genre=Disco URL.</span></span> <span data-ttu-id="3ea73-201">Aşağıda gösterildiği gibi, gözden geçirme sayfasını görüyoruz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-201">We'll see the Browse page displayed like below.</span></span>

![](mvc-music-store-part-3/_static/image16.png)

<span data-ttu-id="3ea73-202">Son olarak, **Depolama dizini** eylem yöntemine biraz daha karmaşık bir güncelleştirme yapalim ve mağazamızda tüm tarzın bir listesini görüntülemek için görünümü.</span><span class="sxs-lookup"><span data-stu-id="3ea73-202">Finally, let's make a slightly more complex update to the **Store Index** action method and view to display a list of all the Genres in our store.</span></span> <span data-ttu-id="3ea73-203">Yalnızca tek bir tarz yerine model nesnemiz olarak bir tarzın listesini kullanarak bunu yapacağız.</span><span class="sxs-lookup"><span data-stu-id="3ea73-203">We'll do that by using a List of Genres as our model object, rather than just a single Genre.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

<span data-ttu-id="3ea73-204">Depolama dizini eylem yöntemine sağ tıklayın ve Görünüm Ekle ' yi seçin, model sınıfı olarak tarz ' ı seçin ve Ekle düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="3ea73-204">Right-click in the Store Index action method and select Add View as before, select Genre as the Model class, and press the Add button.</span></span>

![](mvc-music-store-part-3/_static/image17.png)

<span data-ttu-id="3ea73-205">İlk olarak, görünümün yalnızca bir tane yerine birkaç tarz nesne isteyeceğini göstermek için @model bildirimini değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-205">First we'll change the @model declaration to indicate that the view will be expecting several Genre objects rather than just one.</span></span> <span data-ttu-id="3ea73-206">/Store/Index.cshtml adlı ilk satırı aşağıdaki gibi okunacak şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3ea73-206">Change the first line of /Store/Index.cshtml to read as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

<span data-ttu-id="3ea73-207">Bu, Razor görünüm altyapısına, çeşitli tarz nesneleri tutabilecek bir model nesnesiyle çalışmayacağını söyler.</span><span class="sxs-lookup"><span data-stu-id="3ea73-207">This tells the Razor view engine that it will be working with a model object that can hold several Genre objects.</span></span> <span data-ttu-id="3ea73-208">Daha genel olduğundan, model türümüzü daha sonra IEnumerable arabirimini destekleyen herhangi bir nesne türüne değiştirebilmemiz için, bir liste&lt;tarzı&gt; yerine IEnumerable&lt;tarz&gt; kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-208">We're using an IEnumerable&lt;Genre&gt; rather than a List&lt;Genre&gt; since it's more generic, allowing us to change our model type later to any object type that supports the IEnumerable interface.</span></span>

<span data-ttu-id="3ea73-209">Daha sonra, aşağıdaki tamamlanan görünüm kodunda gösterildiği gibi modeldeki tarz nesneleri arasında döngü göndereceğiz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-209">Next, we'll loop through the Genre objects in the model as shown in the completed view code below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

<span data-ttu-id="3ea73-210">"@Model" yazdığımızda, bu kodu girdiğimiz için tam IntelliSense desteğine sahip olduğumuz hakkında dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="3ea73-210">Notice that we have full IntelliSense support as we enter this code, so that when we type "@Model."</span></span> <span data-ttu-id="3ea73-211">tür tarzı IEnumerable tarafından desteklenen tüm yöntemleri ve özellikleri görüyoruz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-211">we see all methods and properties supported by an IEnumerable of type Genre.</span></span>

![](mvc-music-store-part-3/_static/image18.png)

<span data-ttu-id="3ea73-212">"Foreach" döngümiz dahilinde, Visual Web Developer her öğenin tarz türünde olduğunu bilir, bu nedenle her tarz türü için IntelliSense 'i görüyoruz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-212">Within our "foreach" loop, Visual Web Developer knows that each item is of type Genre, so we see IntelliSense for each the Genre type.</span></span>

![](mvc-music-store-part-3/_static/image19.png)

<span data-ttu-id="3ea73-213">Daha sonra, yapı iskelesi özelliği tarz nesnesini inceledi ve her birinin bir Name özelliğine sahip olduğunu tespit eder, bu nedenle aralarında geçiş yapın ve yazar. Ayrıca, her bir öğe için düzenleme, Ayrıntılar ve silme bağlantıları da oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3ea73-213">Next, the scaffolding feature examined the Genre object and determined that each will have a Name property, so it loops through and writes them out. It also generates Edit, Details, and Delete links to each individual item.</span></span> <span data-ttu-id="3ea73-214">Daha sonra Store Manager 'da bundan sonra faydalanıyoruz, ancak şimdilik basit bir liste kullanmak istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-214">We'll take advantage of that later in our store manager, but for now we'd like to have a simple list instead.</span></span>

<span data-ttu-id="3ea73-215">Uygulamayı çalıştırıp/Store 'a gözattığınızda, her iki tür için de sayım listesinin görüntülendiğini görüyoruz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-215">When we run the application and browse to /Store, we see that both the count and list of Genres is displayed.</span></span>

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a><span data-ttu-id="3ea73-216">Sayfalar arasında bağlantı ekleme</span><span class="sxs-lookup"><span data-stu-id="3ea73-216">Adding Links between pages</span></span>

<span data-ttu-id="3ea73-217">Tarzımızı listeleyen/Store URL 'SI Şu anda yalnızca düz metin olarak tarz adlarını listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-217">Our /Store URL that lists Genres currently lists the Genre names simply as plain text.</span></span> <span data-ttu-id="3ea73-218">Bunu, düz metin yerine uygun/Store/gözam URL 'sine sahip olacak şekilde değiştirelim. böylece, "Disco" gibi bir müzik tarzında tıklatmak/Store/gözatmaya mi? tarzı = disco URL 'sine gidecektir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-218">Let's change this so that instead of plain text we instead have the Genre names link to the appropriate /Store/Browse URL, so that clicking on a music genre like "Disco" will navigate to the /Store/Browse?genre=Disco URL.</span></span> <span data-ttu-id="3ea73-219">Aşağıdaki kodu kullanarak bu bağlantıları çıkarmak için \Views\store\ındex.cshtml görünüm şablonumuzu güncelleştirebiliriz **(bunun üzerinde iyileştireceğiz)** :</span><span class="sxs-lookup"><span data-stu-id="3ea73-219">We could update our \Views\Store\Index.cshtml View template to output these links using code like below **(don't type this in - we're going to improve on it)**:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

<span data-ttu-id="3ea73-220">Bu, daha sonra, sorunsuz kodlanmış bir dizeye dayandığından sorun oluşmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-220">That works, but it could lead to trouble later since it relies on a hardcoded string.</span></span> <span data-ttu-id="3ea73-221">Örneğin, denetleyiciyi yeniden adlandırmak istiyoruz, güncelleştirilebilmemiz gereken bağlantıları arayan kodunuzda arama yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-221">For instance, if we wanted to rename the Controller, we'd need to search through our code looking for links that need to be updated.</span></span>

<span data-ttu-id="3ea73-222">Bir alternatif yaklaşım, bir HTML yardımcı yönteminden faydalanabilir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-222">An alternative approach we can use is to take advantage of an HTML Helper method.</span></span> <span data-ttu-id="3ea73-223">ASP.NET MVC, görüntüleme şablonu kodumuzda olduğu gibi çeşitli yaygın görevleri gerçekleştirmek için kullanılabilen HTML Yardımcısı yöntemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-223">ASP.NET MVC includes HTML Helper methods which are available from our View template code to perform a variety of common tasks just like this.</span></span> <span data-ttu-id="3ea73-224">HTML. ActionLink () yardımcı yöntemi özellikle yararlıdır ve HTML &lt;&gt; bağlantıları oluşturmayı kolaylaştırır ve URL yollarının düzgün şekilde URL kodlamalı olduğundan emin olmak için bu ayrıntıları ele alır.</span><span class="sxs-lookup"><span data-stu-id="3ea73-224">The Html.ActionLink() helper method is a particularly useful one, and makes it easy to build HTML &lt;a&gt; links and takes care of annoying details like making sure URL paths are properly URL encoded.</span></span>

<span data-ttu-id="3ea73-225">HTML. ActionLink (), bağlantılarınız için ihtiyaç duyduğunuz kadar çok bilgi belirtilmesine izin veren birkaç farklı aşırı yüklemeye sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3ea73-225">Html.ActionLink() has several different overloads to allow specifying as much information as you need for your links.</span></span> <span data-ttu-id="3ea73-226">En basit durumda, köprünün istemcide tıklandığı zaman gitmek için yalnızca bağlantı metnini ve eylem yöntemini sağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="3ea73-226">In the simplest case, you'll supply just the link text and the Action method to go to when the hyperlink is clicked on the client.</span></span> <span data-ttu-id="3ea73-227">Örneğin, mağaza ayrıntıları sayfasındaki "/Store/" dizinine bağlantı metni "Store dizinine git" bağlantısını, aşağıdaki çağrıyı kullanarak bağlayabiliriz:</span><span class="sxs-lookup"><span data-stu-id="3ea73-227">For example, we can link to "/Store/" Index() method on the Store Details page with the link text "Go to the Store Index" using the following call:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

<span data-ttu-id="3ea73-228">*Note: Bu durumda, yalnızca geçerli görünümü işleyen Denetleyici içindeki başka bir eyleme bağlanmakta olduğumuz için denetleyici adını belirtmemiz gerekmiyordu.*</span><span class="sxs-lookup"><span data-stu-id="3ea73-228">*Note: In this case, we didn't need to specify the controller name because we're just linking to another action within the same controller that's rendering the current view.*</span></span>

<span data-ttu-id="3ea73-229">Tarama sayfasına yönelik bağlantılarımız bir parametre geçirmemiz gerekir, ancak üç parametre alan HTML. ActionLink yönteminin başka bir aşırı yüklemesini kullanacağız:</span><span class="sxs-lookup"><span data-stu-id="3ea73-229">Our links to the Browse page will need to pass a parameter, though, so we'll use another overload of the Html.ActionLink method that takes three parameters:</span></span>

- 1. <span data-ttu-id="3ea73-230">Bağlantı metni, bu tarz adı görüntülenecektir</span><span class="sxs-lookup"><span data-stu-id="3ea73-230">Link text, which will display the Genre name</span></span>
- 2. <span data-ttu-id="3ea73-231">Denetleyici eylem adı (tarama)</span><span class="sxs-lookup"><span data-stu-id="3ea73-231">Controller action name (Browse)</span></span>
- 3. <span data-ttu-id="3ea73-232">Ad (tarz) ve değer (tarzı adı) belirterek rota parametre değerleri</span><span class="sxs-lookup"><span data-stu-id="3ea73-232">Route parameter values, specifying both the name (Genre) and the value (Genre name)</span></span>

<span data-ttu-id="3ea73-233">Bunu bir araya getirmek, bu bağlantıları mağaza dizini görünümüne yazdığımızda şöyle olacaktır:</span><span class="sxs-lookup"><span data-stu-id="3ea73-233">Putting that all together, here's how we'll write those links to the Store Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

<span data-ttu-id="3ea73-234">Şimdi projemizi yeniden çalıştırıp/Store/URL 'ye eriştiğinizde, tarzın bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3ea73-234">Now when we run our project again and access the /Store/ URL we will see a list of genres.</span></span> <span data-ttu-id="3ea73-235">Her bir tarz bir köprüdür. tıklandıklarında, bu bir köprü,/Store/gözatmaya mi? tarzı = *[tarz]* URL 'imize götürür.</span><span class="sxs-lookup"><span data-stu-id="3ea73-235">Each genre is a hyperlink – when clicked it will take us to our /Store/Browse?genre=*[genre]* URL.</span></span>

![](mvc-music-store-part-3/_static/image3.jpg)

<span data-ttu-id="3ea73-236">Tarz listesinin HTML 'si şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="3ea73-236">The HTML for the genre list looks like this:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> <span data-ttu-id="3ea73-237">[Önceki](mvc-music-store-part-2.md)
> [İleri](mvc-music-store-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="3ea73-237">[Previous](mvc-music-store-part-2.md)
[Next](mvc-music-store-part-4.md)</span></span>
