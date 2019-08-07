---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: Denetleyici ekleme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 6b38d757d37374b14979f8a079a46158ff64f9c3
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810771"
---
# <a name="adding-a-controller"></a><span data-ttu-id="7ee05-102">Denetleyici Ekleme</span><span class="sxs-lookup"><span data-stu-id="7ee05-102">Adding a Controller</span></span>

<span data-ttu-id="7ee05-103">[Rick Anderson]((https://twitter.com/RickAndMSFT)) tarafından</span><span class="sxs-lookup"><span data-stu-id="7ee05-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="7ee05-104">MVC, *Model-View-Controller*için temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7ee05-104">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="7ee05-105">MVC, iyi şekilde tasarlanmış ve bakımı kolay olan uygulamalar geliştirmeye yönelik bir modeldir.</span><span class="sxs-lookup"><span data-stu-id="7ee05-105">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="7ee05-106">MVC tabanlı uygulamalar şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="7ee05-106">MVC-based applications contain:</span></span>

- <span data-ttu-id="7ee05-107">**A** odels: Uygulamanın verilerini temsil eden ve bu veriler için iş kurallarını zorlamak üzere doğrulama mantığını kullanan sınıflar.</span><span class="sxs-lookup"><span data-stu-id="7ee05-107">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="7ee05-108">**V** ıews: Uygulamanızın, dinamik olarak HTML yanıtları oluşturmak için kullandığı şablon dosyaları.</span><span class="sxs-lookup"><span data-stu-id="7ee05-108">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="7ee05-109">**C** ontrolleyiciler: Gelen tarayıcı isteklerini işleyen sınıflar, model verilerini alır ve tarayıcıya yanıt döndüren şablonları görüntüle seçeneğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7ee05-109">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="7ee05-110">Bu öğretici serisinde bu kavramların tümünü ele alacağız ve bir uygulama oluşturmak için bunları nasıl kullanacağınızı göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="7ee05-110">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="7ee05-111">Bir denetleyici sınıfı oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="7ee05-111">Let's begin by creating a controller class.</span></span> <span data-ttu-id="7ee05-112">**Çözüm Gezgini**, *denetleyiciler* klasörüne sağ tıklayın ve ardından **Ekle**' ye ve ardından **Denetleyici**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7ee05-112">In **Solution Explorer**, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="7ee05-113">**Yapı Iskelesi Ekle** Iletişim kutusunda **MVC 5 denetleyici-boş**' ya tıklayın ve ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7ee05-113">In the **Add Scaffold** dialog box, click **MVC 5 Controller - Empty**, and then click **Add**.</span></span>

![](adding-a-controller/_static/image2.png)  

<span data-ttu-id="7ee05-114">Yeni denetleyicinizi "Merhaba Dünya denetleyicisi" olarak adlandırın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7ee05-114">Name your new controller "HelloWorldController" and click **Add**.</span></span>

![denetleyici Ekle](adding-a-controller/_static/image3.png)

<span data-ttu-id="7ee05-116">**Çözüm Gezgini** , *HelloWorldController.cs* adlı yeni bir dosya ve *views\helloworld*adlı yeni bir klasör oluşturulduğunu fark edin.</span><span class="sxs-lookup"><span data-stu-id="7ee05-116">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs* and a new folder *Views\HelloWorld*.</span></span> <span data-ttu-id="7ee05-117">Denetleyici IDE 'de açıktır.</span><span class="sxs-lookup"><span data-stu-id="7ee05-117">The controller is open in the IDE.</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="7ee05-118">Dosyanın içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7ee05-118">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="7ee05-119">Denetleyici yöntemleri bir örnek olarak HTML dizesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="7ee05-119">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="7ee05-120">Denetleyici adlandırılır `HelloWorldController` ve ilk yöntem adlandırılır `Index`.</span><span class="sxs-lookup"><span data-stu-id="7ee05-120">The controller is named `HelloWorldController` and the first method is named `Index`.</span></span> <span data-ttu-id="7ee05-121">Bir tarayıcıdan çağıralım.</span><span class="sxs-lookup"><span data-stu-id="7ee05-121">Let's invoke it from a browser.</span></span> <span data-ttu-id="7ee05-122">Uygulamayı çalıştırın (F5 tuşuna basın veya CTRL + F5 tuşlarına basın).</span><span class="sxs-lookup"><span data-stu-id="7ee05-122">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="7ee05-123">Tarayıcıda, adres çubuğundaki yola &quot;HelloWorld&quot; ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7ee05-123">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="7ee05-124">(Örneğin, aşağıdaki çizimde olduğu `http://localhost:1234/HelloWorld.`gibi), tarayıcıdaki sayfa aşağıdaki ekran görüntüsüne benzer şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="7ee05-124">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="7ee05-125">Yukarıdaki yöntemde kod doğrudan bir dize döndürdü.</span><span class="sxs-lookup"><span data-stu-id="7ee05-125">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="7ee05-126">Sisteme yalnızca birkaç HTML döndürdüyordu ve!</span><span class="sxs-lookup"><span data-stu-id="7ee05-126">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="7ee05-127">ASP.NET MVC, gelen URL 'ye bağlı olarak farklı denetleyici sınıflarını (ve bunların içinde farklı eylem yöntemlerini) çağırır.</span><span class="sxs-lookup"><span data-stu-id="7ee05-127">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="7ee05-128">ASP.NET MVC tarafından kullanılan varsayılan URL yönlendirme mantığı, çağrılacak kodu belirlemek için aşağıdaki gibi bir biçim kullanır:</span><span class="sxs-lookup"><span data-stu-id="7ee05-128">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="7ee05-129">*Uygulama\_başlangıç/routeconfig. cs* dosyasında yönlendirme biçimini ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="7ee05-129">You set the format for routing in the *App\_Start/RouteConfig.cs* file.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

<span data-ttu-id="7ee05-130">Uygulamayı çalıştırdığınızda ve herhangi bir URL kesimini sağlamadığınızda, varsayılan olarak "giriş" denetleyicisi ve Yukarıdaki kodun varsayılanlar bölümünde belirtilen "Dizin" eylem yöntemi olur.</span><span class="sxs-lookup"><span data-stu-id="7ee05-130">When you run the application and don't supply any URL segments, it defaults to the "Home" controller and the "Index" action method specified in the defaults section of the code above.</span></span>

<span data-ttu-id="7ee05-131">URL 'nin ilk bölümü yürütülecek denetleyici sınıfını belirler.</span><span class="sxs-lookup"><span data-stu-id="7ee05-131">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="7ee05-132">Bu nedenle */HelloWorld* `HelloWorldController` sınıfla eşlenir.</span><span class="sxs-lookup"><span data-stu-id="7ee05-132">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="7ee05-133">URL 'nin ikinci bölümü, yürütülecek sınıftaki Action metodunu belirler.</span><span class="sxs-lookup"><span data-stu-id="7ee05-133">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="7ee05-134">Bu nedenle */HelloWorld/Index* `Index` `HelloWorldController` sınıfın yönteminin yürütülmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="7ee05-134">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="7ee05-135">Yalnızca */HelloWorld* öğesine göz atabildiğimiz ve `Index` yöntemin varsayılan olarak kullanıldığı konusunda dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7ee05-135">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="7ee05-136">Bunun nedeni, bir yöntemi `Index` açıkça belirtilmediyse bir denetleyicide çağrılacak olan varsayılan yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="7ee05-136">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span> <span data-ttu-id="7ee05-137">URL segmentinin ( `Parameters`) üçüncü bölümü rota verileri içindir.</span><span class="sxs-lookup"><span data-stu-id="7ee05-137">The third part of the URL segment ( `Parameters`) is for route data.</span></span> <span data-ttu-id="7ee05-138">Bu öğreticide daha sonra rota verilerini inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="7ee05-138">We'll see route data later on in this tutorial.</span></span>

<span data-ttu-id="7ee05-139">konumuna gözatın `http://localhost:xxxx/HelloWorld/Welcome`.</span><span class="sxs-lookup"><span data-stu-id="7ee05-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="7ee05-140">Yöntemi çalışır ve bu karşılama eylemi yöntemi &quot;olan dizeyi döndürür... `Welcome` &quot;.</span><span class="sxs-lookup"><span data-stu-id="7ee05-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="7ee05-141">Varsayılan MVC eşlemesi `/[Controller]/[ActionName]/[Parameters]`.</span><span class="sxs-lookup"><span data-stu-id="7ee05-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="7ee05-142">Bu URL için denetleyici `HelloWorld` , ve `Welcome` eylem yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="7ee05-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="7ee05-143">URL 'nin bir `[Parameters]` bölümünü henüz kullanmadınız.</span><span class="sxs-lookup"><span data-stu-id="7ee05-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="7ee05-144">URL 'den denetleyiciye bazı parametre bilgilerini geçirebilmeniz için örneği biraz daha değiştirelim (örneğin, */HelloWorld/Welcome? ad = Scott&amp;numtimes = 4*).</span><span class="sxs-lookup"><span data-stu-id="7ee05-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="7ee05-145">`Welcome` Yönteminizi aşağıda gösterildiği gibi iki parametre içerecek şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7ee05-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="7ee05-146">Bu parametre için hiçbir değer geçirilmemişse, C# `numTimes` kodun varsayılan olarak 1 ' e sahip olacağını belirtmek için isteğe bağlı parametre özelliğini kullandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7ee05-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="7ee05-147">Güvenlik Notno: Yukarıdaki kod, uygulamayı kötü amaçlı girişten korumak için [HttpUtility. HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) kullanır (yani JavaScript).</span><span class="sxs-lookup"><span data-stu-id="7ee05-147">Security Note: The code above uses [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) to protect the application from malicious input (namely JavaScript).</span></span> <span data-ttu-id="7ee05-148">Daha fazla bilgi için [nasıl yapılır: Dizelere](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)HTML kodlaması uygulayarak bir Web uygulamasındaki betiklere karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="7ee05-148">For more information see [How to: Protect Against Script Exploits in a Web Application by Applying HTML Encoding to Strings](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).</span></span>

 <span data-ttu-id="7ee05-149">Uygulamanızı çalıştırın ve örnek URL 'ye (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`) gidin.</span><span class="sxs-lookup"><span data-stu-id="7ee05-149">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`).</span></span> <span data-ttu-id="7ee05-150">URL 'de ve `name` `numtimes` için farklı değerler deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ee05-150">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="7ee05-151">[ASP.NET MVC model bağlama sistemi](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) , adlandırılmış parametreleri adres çubuğundaki sorgu dizesinden yöntemdeki parametrelere otomatik olarak eşler.</span><span class="sxs-lookup"><span data-stu-id="7ee05-151">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="7ee05-152">Yukarıdaki örnekte, `Parameters`URL segmenti () kullanılmaz `name` , ve `numTimes` parametreleri [sorgu dizeleri](http://en.wikipedia.org/wiki/Query_string)olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="7ee05-152">In the sample above, the URL segment ( `Parameters`) is not used, the `name` and `numTimes` parameters are passed as [query strings](http://en.wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="7ee05-153">İçin?</span><span class="sxs-lookup"><span data-stu-id="7ee05-153">The ?</span></span> <span data-ttu-id="7ee05-154">(soru işareti) Yukarıdaki URL 'de bir ayırıcıdır ve sorgu dizeleri aşağıdaki gibi olur.</span><span class="sxs-lookup"><span data-stu-id="7ee05-154">(question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="7ee05-155">&amp; Karakter Sorgu dizelerini ayırır.</span><span class="sxs-lookup"><span data-stu-id="7ee05-155">The &amp; character separates query strings.</span></span>

<span data-ttu-id="7ee05-156">Welcome metodunu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7ee05-156">Replace the Welcome method with the following code:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

<span data-ttu-id="7ee05-157">Uygulamayı çalıştırın ve aşağıdaki URL 'YI girin:`http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span><span class="sxs-lookup"><span data-stu-id="7ee05-157">Run the application and enter the following URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="7ee05-158">Bu kez, üçüncü URL `ID.` segmenti, `RegisterRoutes` yöntemi içindeki URL belirtimiyle `Welcome` eşleşen bir parametreyi (`ID`) içeren yol parametresiyle eşleştirildiği zaman.</span><span class="sxs-lookup"><span data-stu-id="7ee05-158">This time the third URL segment matched the route parameter `ID.` The `Welcome` action method contains a parameter (`ID`) that matched the URL specification in the `RegisterRoutes` method.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

<span data-ttu-id="7ee05-159">ASP.NET MVC uygulamalarında, parametreleri sorgu dizeleri olarak geçirmeden, parametreleri yönlendirme verileri (yukarıda ID ile yaptığımız gibi) olarak geçirmek daha tipik bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="7ee05-159">In ASP.NET MVC applications, it's more typical to pass in parameters as route data (like we did with ID above) than passing them as query strings.</span></span> <span data-ttu-id="7ee05-160">Ayrıca, `name` `numtimes` URL 'ye yönlendirme verileri olarak hem hem de parametrelerini geçirmek için bir yol ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ee05-160">You could also add a route to pass both the `name` and `numtimes` in parameters as route data in the URL.</span></span> <span data-ttu-id="7ee05-161">*App\_start\routeconfig.cs* dosyasına "Merhaba" yolunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7ee05-161">In the *App\_Start\RouteConfig.cs* file, add the "Hello" route:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

<span data-ttu-id="7ee05-162">Uygulamayı çalıştırın ve konumuna gidin `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span><span class="sxs-lookup"><span data-stu-id="7ee05-162">Run the application and browse to `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span></span>

![](adding-a-controller/_static/image9.png)

<span data-ttu-id="7ee05-163">Birçok MVC uygulaması için, varsayılan yol sorunsuz şekilde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="7ee05-163">For many MVC applications, the default route works fine.</span></span> <span data-ttu-id="7ee05-164">Bu öğreticide daha sonra model cildi kullanarak veri geçireceğini öğrenirsiniz ve bunun için varsayılan yolu değiştirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7ee05-164">You'll learn later in this tutorial to pass data using the model binder, and you won't have to modify the default route for that.</span></span>

<span data-ttu-id="7ee05-165">Bu örneklerde, denetleyici MVC 'nin &quot;VC&quot; bölümünü yapıyor — yani, görünüm ve denetleyici çalışır.</span><span class="sxs-lookup"><span data-stu-id="7ee05-165">In these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="7ee05-166">Denetleyici HTML 'i doğrudan döndürüyor.</span><span class="sxs-lookup"><span data-stu-id="7ee05-166">The controller is returning HTML directly.</span></span> <span data-ttu-id="7ee05-167">Normalde, kod için çok daha fazla hale geldiği için denetleyicilerin doğrudan HTML döndürmesini istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ee05-167">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="7ee05-168">Bunun yerine, genellikle HTML yanıtı oluşturmaya yardımcı olmak için ayrı bir görünüm şablonu dosyası kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="7ee05-168">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="7ee05-169">Şimdi bunu nasıl yapadığımızda bakalım.</span><span class="sxs-lookup"><span data-stu-id="7ee05-169">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7ee05-170">[Önceki](getting-started.md)İleri
> [](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="7ee05-170">[Previous](getting-started.md)
[Next](adding-a-view.md)</span></span>
