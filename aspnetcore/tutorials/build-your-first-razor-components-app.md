---
title: Razor bileşenleri ilk uygulamanızı oluşturun
author: guardrex
description: Adım adım bir Razor bileşenleri uygulaması derleme ve Razor bileşenleri temel kavramları öğrenin.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/11/2019
uid: tutorials/first-razor-components-app
ms.openlocfilehash: 0c3dd2366581d73bad44e2911602e13c6c0daf9a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070872"
---
# <a name="build-your-first-razor-components-app"></a><span data-ttu-id="d6ede-103">Razor bileşenleri ilk uygulamanızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="d6ede-103">Build your first Razor Components app</span></span>

<span data-ttu-id="d6ede-104">Tarafından [Daniel Roth](https://github.com/danroth27) ve [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="d6ede-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="d6ede-105">Bu öğretici, Razor bileşenleri ile uygulama oluşturma işlemini göstermektedir ve Razor bileşenleri temel kavramlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6ede-105">This tutorial shows you how to build an app with Razor Components and demonstrates basic Razor Components concepts.</span></span> <span data-ttu-id="d6ede-106">Bu öğretici (.NET Core 3.0 veya sonraki sürümlerde desteklenir) ya da bir Razor bileşenleri tabanlı proje veya (.NET Core gelecekteki bir sürümde desteklenir) Blazor tabanlı bir proje kullanarak keyfini çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6ede-106">You can enjoy this tutorial using either a Razor Components-based project (supported in .NET Core 3.0 or later) or using a Blazor-based project (supported in a future release of .NET Core).</span></span>

<span data-ttu-id="d6ede-107">ASP.NET Core Razor bileşenlerini kullanarak bir deneyim için (*önerilen*):</span><span class="sxs-lookup"><span data-stu-id="d6ede-107">For an experience using ASP.NET Core Razor Components (*recommended*):</span></span>

* <span data-ttu-id="d6ede-108">Sunulan yönergeleri <xref:razor-components/get-started> Razor bileşenleri tabanlı bir proje oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d6ede-108">Follow the guidance in <xref:razor-components/get-started> to create a Razor Components-based project.</span></span>
* <span data-ttu-id="d6ede-109">Projeyi adlandırın `RazorComponents`.</span><span class="sxs-lookup"><span data-stu-id="d6ede-109">Name the project `RazorComponents`.</span></span>
* <span data-ttu-id="d6ede-110">Bir çoklu proje çözümü Razor bileşenleri şablonu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d6ede-110">A multi-project solution is created from the Razor Components template.</span></span> <span data-ttu-id="d6ede-111">Razor bileşenleri proje olarak oluşturulan *RazorComponents.App*.</span><span class="sxs-lookup"><span data-stu-id="d6ede-111">The Razor Components project is generated as *RazorComponents.App*.</span></span>

<span data-ttu-id="d6ede-112">Blazor kullanarak bir deneyim için:</span><span class="sxs-lookup"><span data-stu-id="d6ede-112">For an experience using Blazor:</span></span>

* <span data-ttu-id="d6ede-113">Sunulan yönergeleri <xref:spa/blazor/get-started> Blazor tabanlı bir proje oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d6ede-113">Follow the guidance in <xref:spa/blazor/get-started> to create a Blazor-based project.</span></span>
* <span data-ttu-id="d6ede-114">Projeyi adlandırın `Blazor`.</span><span class="sxs-lookup"><span data-stu-id="d6ede-114">Name the project `Blazor`.</span></span>
* <span data-ttu-id="d6ede-115">Bir tek proje çözüm Blazor şablonu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d6ede-115">A single-project solution is created from the Blazor template.</span></span>

<span data-ttu-id="d6ede-116">[Görüntüleme veya indirme örnek kodu](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/build-your-first-razor-components-app/samples/) ([nasıl indirileceğini](xref:index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="d6ede-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/build-your-first-razor-components-app/samples/) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="d6ede-117">Önkoşullar için aşağıdaki konulara bakın:</span><span class="sxs-lookup"><span data-stu-id="d6ede-117">See the following topics for prerequisites:</span></span>

## <a name="build-components"></a><span data-ttu-id="d6ede-118">Yapı bileşenleri</span><span class="sxs-lookup"><span data-stu-id="d6ede-118">Build components</span></span>

1. <span data-ttu-id="d6ede-119">Her bir uygulamanın üç göz atın: Giriş, sayaç ve veri getirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="d6ede-119">Browse to each of the app's three pages: Home, Counter, and Fetch data.</span></span> <span data-ttu-id="d6ede-120">Bu sayfalar, Razor dosyalarında tarafından uygulanan *sayfaları* klasörü: *Index.cshtml*, *Counter.cshtml*, ve *FetchData.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="d6ede-120">These pages are implemented by Razor files in the *Pages* folder: *Index.cshtml*, *Counter.cshtml*, and *FetchData.cshtml*.</span></span>

1. <span data-ttu-id="d6ede-121">Sayaç sayfasında **me tıklayın** sayfa yenileme olmadan sayaç artmaya düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d6ede-121">On the Counter page, select the **Click me** button to increment the counter without a page refresh.</span></span> <span data-ttu-id="d6ede-122">Normal olarak artan bir Web sayfasındaki bir sayaç JavaScript Yazma gerektiriyor, ancak Razor bileşenleri sağlayan daha iyi bir yaklaşım kullanarak C#.</span><span class="sxs-lookup"><span data-stu-id="d6ede-122">Incrementing a counter in a webpage normally requires writing JavaScript, but Razor Components provides a better approach using C#.</span></span>

1. <span data-ttu-id="d6ede-123">Uygulama sayacı bileşenin inceleyin *Counter.cshtml* dosya.</span><span class="sxs-lookup"><span data-stu-id="d6ede-123">Examine the implementation of the Counter component in the *Counter.cshtml* file.</span></span>

   <span data-ttu-id="d6ede-124">*Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="d6ede-124">*Pages/Counter.cshtml*:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Counter1.cshtml)]

   <span data-ttu-id="d6ede-125">Kullanıcı arabirimini sayacı bileşenin HTML kullanılarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d6ede-125">The UI of the Counter component is defined using HTML.</span></span> <span data-ttu-id="d6ede-126">(Örneğin, döngü, koşullular, ifadeleri) dinamik işleme mantığı, katıştırılmış kullanarak eklenir C# adlı söz dizimi [Razor](xref:mvc/views/razor).</span><span class="sxs-lookup"><span data-stu-id="d6ede-126">Dynamic rendering logic (for example, loops, conditionals, expressions) is added using an embedded C# syntax called [Razor](xref:mvc/views/razor).</span></span> <span data-ttu-id="d6ede-127">HTML biçimlendirmesi ve C# işleme mantığı, oluşturma zamanında bir bileşen sınıfı dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="d6ede-127">The HTML markup and C# rendering logic are converted into a component class at build time.</span></span> <span data-ttu-id="d6ede-128">Oluşturulan .NET sınıf adı dosya adıyla eşleşen.</span><span class="sxs-lookup"><span data-stu-id="d6ede-128">The name of the generated .NET class matches the file name.</span></span>

   <span data-ttu-id="d6ede-129">Bileşen sınıfı üyeleri tanımlanmış bir `@functions` blok.</span><span class="sxs-lookup"><span data-stu-id="d6ede-129">Members of the component class are defined in a `@functions` block.</span></span> <span data-ttu-id="d6ede-130">İçinde `@functions` blok, bileşen durumu (Özellikler, alanlar) ve olay işleme için veya başka bir bileşen mantığı tanımlamak için yöntemleri belirtilir.</span><span class="sxs-lookup"><span data-stu-id="d6ede-130">In the `@functions` block, component state (properties, fields) and methods are specified for event handling or for defining other component logic.</span></span> <span data-ttu-id="d6ede-131">Bu üyeleri, ardından bileşenin işleme mantığı ve olayları işlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d6ede-131">These members are then used as part of the component's rendering logic and for handling events.</span></span>

   <span data-ttu-id="d6ede-132">Zaman **me tıklayın** düğmesi seçili:</span><span class="sxs-lookup"><span data-stu-id="d6ede-132">When the **Click me** button is selected:</span></span>

   * <span data-ttu-id="d6ede-133">Sayaç bileşen kayıtlı `onclick` işleyici çağrılır ( `IncrementCount` yöntemi).</span><span class="sxs-lookup"><span data-stu-id="d6ede-133">The Counter component's registered `onclick` handler is called (the `IncrementCount` method).</span></span>
   * <span data-ttu-id="d6ede-134">Sayaç bileşen kendi işleme ağacında yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d6ede-134">The Counter component regenerates its render tree.</span></span>
   * <span data-ttu-id="d6ede-135">Yeni bir işleme ağacı Öncekine karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="d6ede-135">The new render tree is compared to the previous one.</span></span>
   * <span data-ttu-id="d6ede-136">Yalnızca belge nesne modeli (DOM) değişiklikler uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d6ede-136">Only modifications to the Document Object Model (DOM) are applied.</span></span> <span data-ttu-id="d6ede-137">Görüntülenen sayısı güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d6ede-137">The displayed count is updated.</span></span>

1. <span data-ttu-id="d6ede-138">Değiştirme C# bir yerine ikiye sayısı artması yapmak için sayaç bileşeninin mantığı.</span><span class="sxs-lookup"><span data-stu-id="d6ede-138">Modify the C# logic of the Counter component to make the count increment by two instead of one.</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Counter2.cshtml?highlight=14)]

1. <span data-ttu-id="d6ede-139">Yeniden oluşturun ve değişiklikleri görmek için uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d6ede-139">Rebuild and run the app to see the changes.</span></span> <span data-ttu-id="d6ede-140">Seçin **me tıklayın** düğmeyi ve iki sayacını artırır.</span><span class="sxs-lookup"><span data-stu-id="d6ede-140">Select the **Click me** button, and the counter increments by two.</span></span>

## <a name="use-components"></a><span data-ttu-id="d6ede-141">Bileşenleri kullanma</span><span class="sxs-lookup"><span data-stu-id="d6ede-141">Use components</span></span>

<span data-ttu-id="d6ede-142">Bir HTML benzeri sözdizimi kullanarak başka bir bileşene dönüştürerek bileşen içerir.</span><span class="sxs-lookup"><span data-stu-id="d6ede-142">Include a component into another component using an HTML-like syntax.</span></span>

1. <span data-ttu-id="d6ede-143">Sayaç bileşen uygulamanın dizini (giriş sayfası) bileşenine ekleyerek bir `<Counter />` dizin bileşeni öğesi.</span><span class="sxs-lookup"><span data-stu-id="d6ede-143">Add the Counter component to the app's Index (home page) component by adding a `<Counter />` element to the Index component.</span></span>

   <span data-ttu-id="d6ede-144">Bu deneyim için bir anket istemi bileşeni Blazor kullanıyorsanız (`<SurveyPrompt>` öğesi) dizin bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="d6ede-144">If you're using Blazor for this experience, a Survey Prompt component (`<SurveyPrompt>` element) is in the Index component.</span></span> <span data-ttu-id="d6ede-145">Değiştirin `<SurveyPrompt>` öğeyle `<Counter>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="d6ede-145">Replace the `<SurveyPrompt>` element with the `<Counter>` element.</span></span>

   <span data-ttu-id="d6ede-146">*Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="d6ede-146">*Pages/Index.cshtml*:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Index.cshtml?highlight=7)]

1. <span data-ttu-id="d6ede-147">Yeniden oluşturun ve uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d6ede-147">Rebuild and run the app.</span></span> <span data-ttu-id="d6ede-148">Giriş sayfası, kendi sayaç vardır.</span><span class="sxs-lookup"><span data-stu-id="d6ede-148">The home page has its own counter.</span></span>

## <a name="component-parameters"></a><span data-ttu-id="d6ede-149">Bileşen parametreleri</span><span class="sxs-lookup"><span data-stu-id="d6ede-149">Component parameters</span></span>

<span data-ttu-id="d6ede-150">Bileşenleri parametrelerini de sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6ede-150">Components can also have parameters.</span></span> <span data-ttu-id="d6ede-151">Bileşen parametreleri, genel olmayan özellikler ile donatılmış bileşen sınıfı kullanarak tanımlanan `[Parameter]`.</span><span class="sxs-lookup"><span data-stu-id="d6ede-151">Component parameters are defined using non-public properties on the component class decorated with `[Parameter]`.</span></span> <span data-ttu-id="d6ede-152">Öznitelikleri bir bileşen için bağımsız değişken biçimlendirme içinde belirtmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6ede-152">Use attributes to specify arguments for a component in markup.</span></span>

1. <span data-ttu-id="d6ede-153">Bileşenin güncelleştirme `@functions` C# kod:</span><span class="sxs-lookup"><span data-stu-id="d6ede-153">Update the component's `@functions` C# code:</span></span>

   * <span data-ttu-id="d6ede-154">Ekleme bir `IncrementAmount` özelliği düzenlenmiş ile `[Parameter]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="d6ede-154">Add a `IncrementAmount` property decorated with the `[Parameter]` attribute.</span></span>
   * <span data-ttu-id="d6ede-155">Değişiklik `IncrementCount` yönteminin kullanılacağını `IncrementAmount` değerini artırmayı olduğunda `currentCount`.</span><span class="sxs-lookup"><span data-stu-id="d6ede-155">Change the `IncrementCount` method to use the `IncrementAmount` when increasing the value of `currentCount`.</span></span>

   <span data-ttu-id="d6ede-156">*Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="d6ede-156">*Pages/Counter.cshtml*:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Counter.cshtml?highlight=12,16)]

<!-- Add back when supported.
   > [!NOTE]
   > From Visual Studio, you can quickly add a component parameter by using the `para` snippet. Type `para` and press the `Tab` key twice.
-->

1. <span data-ttu-id="d6ede-157">Belirtin bir `IncrementAmount` ana bileşenin parametresinde `<Counter>` öğesini kullanarak bir öznitelik.</span><span class="sxs-lookup"><span data-stu-id="d6ede-157">Specify an `IncrementAmount` parameter in the Home component's `<Counter>` element using an attribute.</span></span> <span data-ttu-id="d6ede-158">Sayaç tarafından on Artır bir değere ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d6ede-158">Set the value to increment the counter by ten.</span></span>

   <span data-ttu-id="d6ede-159">*Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="d6ede-159">*Pages/Index.cshtml*:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Index.cshtml?highlight=7)]

1. <span data-ttu-id="d6ede-160">Sayfayı yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d6ede-160">Reload the page.</span></span> <span data-ttu-id="d6ede-161">Giriş sayfası sayaç artırılır on tarafından her zaman **me tıklayın** düğmesi seçili.</span><span class="sxs-lookup"><span data-stu-id="d6ede-161">The home page counter increments by ten each time the **Click me** button is selected.</span></span> <span data-ttu-id="d6ede-162">Sayaca sağ *sayacı* sayfasında artışlarla bir.</span><span class="sxs-lookup"><span data-stu-id="d6ede-162">The counter on the *Counter* page increments by one.</span></span>

## <a name="route-to-components"></a><span data-ttu-id="d6ede-163">Bileşenleri için yol</span><span class="sxs-lookup"><span data-stu-id="d6ede-163">Route to components</span></span>

<span data-ttu-id="d6ede-164">`@page` En üstündeki yönerge *Counter.cshtml* dosya bu bileşen yönlendirme bir uç nokta olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="d6ede-164">The `@page` directive at the top of the *Counter.cshtml* file specifies that this component is a routing endpoint.</span></span> <span data-ttu-id="d6ede-165">Sayaç bileşeni için gönderilen istekleri işler `/Counter`.</span><span class="sxs-lookup"><span data-stu-id="d6ede-165">The Counter component handles requests sent to `/Counter`.</span></span> <span data-ttu-id="d6ede-166">Olmadan `@page` yönergesi, bileşen yönlendirilen istekler da işlemiyor ancak bileşeni hala başka bileşenler tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d6ede-166">Without the `@page` directive, the component doesn't handle routed requests, but the component can still be used by other components.</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="d6ede-167">Bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="d6ede-167">Dependency injection</span></span>

<span data-ttu-id="d6ede-168">Bileşenleri uygulamanın service kapsayıcısında kayıtlı hizmetlerinin kullanılabilir [bağımlılık ekleme (dı)](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="d6ede-168">Services registered in the app's service container are available to components via [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="d6ede-169">Halinde bileşenini kullanarak Hizmetleri ekleme `@inject` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="d6ede-169">Inject services into a component using the `@inject` directive.</span></span>

<span data-ttu-id="d6ede-170">Parçalar bileşenin yönergeleri inceleyin (*Pages/FetchData.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="d6ede-170">Examine the directives of the FetchData component (*Pages/FetchData.cshtml*).</span></span> <span data-ttu-id="d6ede-171">`@inject` Yönergesi örneğini ekleme için kullanılan `WeatherForecastService` hizmet bileşeni içinde:</span><span class="sxs-lookup"><span data-stu-id="d6ede-171">The `@inject` directive is used to inject the instance of the `WeatherForecastService` service into the component:</span></span>

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData1.cshtml?highlight=3)]

<span data-ttu-id="d6ede-172">`WeatherForecastService` Hizmet olarak kayıtlı bir [singleton](xref:fundamentals/dependency-injection#service-lifetimes), Hizmeti'nin bir örneğini uygulama boyunca kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d6ede-172">The `WeatherForecastService` service is registered as a [singleton](xref:fundamentals/dependency-injection#service-lifetimes), so one instance of the service is available throughout the app.</span></span>

<span data-ttu-id="d6ede-173">Parçalar bileşeni olarak eklenen hizmet kullanan `ForecastService`, bir dizi alınacak `WeatherForecast` nesneler:</span><span class="sxs-lookup"><span data-stu-id="d6ede-173">The FetchData component uses the injected service, as `ForecastService`, to retrieve an array of `WeatherForecast` objects:</span></span>

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData2.cshtml?highlight=6)]

<span data-ttu-id="d6ede-174">A [ @foreach ](/dotnet/csharp/language-reference/keywords/foreach-in) döngü, her bir tahmin örneği tablosunda bir satıra hava durumu verilerinin işlemek için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="d6ede-174">A [@foreach](/dotnet/csharp/language-reference/keywords/foreach-in) loop is used to render each forecast instance as a row in the table of weather data:</span></span>

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData3.cshtml?highlight=11-19)]

## <a name="build-a-todo-list"></a><span data-ttu-id="d6ede-175">Bir Yapılacaklar listesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="d6ede-175">Build a todo list</span></span>

<span data-ttu-id="d6ede-176">Bir basit bir Yapılacaklar listesi uygulayan uygulamaya yeni bir sayfa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d6ede-176">Add a new page to the app that implements a simple todo list.</span></span>

1. <span data-ttu-id="d6ede-177">Boş bir dosyaya eklemek *sayfaları* adlı klasöre *Todo.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="d6ede-177">Add an empty file to the *Pages* folder named *Todo.cshtml*.</span></span>

1. <span data-ttu-id="d6ede-178">Sayfa için ilk biçimlendirme sağlar:</span><span class="sxs-lookup"><span data-stu-id="d6ede-178">Provide the initial markup for the page:</span></span>

   ```cshtml
   @page "/todo"

   <h1>Todo</h1>
   ```

1. <span data-ttu-id="d6ede-179">Todo sayfa gezinti çubuğuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d6ede-179">Add the Todo page to the navigation bar.</span></span>

   <span data-ttu-id="d6ede-180">NavMenu bileşeni (*Shared/NavMenu.csthml*) uygulamanın düzende kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d6ede-180">The NavMenu component (*Shared/NavMenu.csthml*) is used in the app's layout.</span></span> <span data-ttu-id="d6ede-181">Düzenleri, uygulama içeriği yinelenmesini önlemek izin bileşenlerdir.</span><span class="sxs-lookup"><span data-stu-id="d6ede-181">Layouts are components that allow you to avoid duplication of content in the app.</span></span> <span data-ttu-id="d6ede-182">Daha fazla bilgi için bkz. <xref:razor-components/layouts>.</span><span class="sxs-lookup"><span data-stu-id="d6ede-182">For more information, see <xref:razor-components/layouts>.</span></span>

   <span data-ttu-id="d6ede-183">Ekleme bir `<NavLink>` için aşağıda bulunan mevcut liste öğelerini aşağıdaki liste öğesi işaretleme ekleyerek Todo sayfası *Shared/NavMenu.csthml* dosyası:</span><span class="sxs-lookup"><span data-stu-id="d6ede-183">Add a `<NavLink>` for the Todo page by adding the following list item markup below the existing list items in the *Shared/NavMenu.csthml* file:</span></span>

   ```cshtml
   <li class="nav-item px-3">
       <NavLink class="nav-link" href="todo">
           <span class="oi oi-list-rich" aria-hidden="true"></span> Todo
       </NavLink>
   </li>
   ```

1. <span data-ttu-id="d6ede-184">Yeniden oluşturun ve uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d6ede-184">Rebuild and run the app.</span></span> <span data-ttu-id="d6ede-185">Todo sayfanın bağlantısını çalıştığını onaylamak için yeni Todo sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="d6ede-185">Visit the new Todo page to confirm that the link to the Todo page works.</span></span>

1. <span data-ttu-id="d6ede-186">Ekleme bir *TodoItem.cs* bir todo öğesini temsil eden bir sınıf tutmak için projenin kök dosya.</span><span class="sxs-lookup"><span data-stu-id="d6ede-186">Add a *TodoItem.cs* file to the root of the project to hold a class that represents a todo item.</span></span> <span data-ttu-id="d6ede-187">Aşağıdaki C# için kod `TodoItem` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="d6ede-187">Use the following C# code for the `TodoItem` class:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/TodoItem.cs)]

1. <span data-ttu-id="d6ede-188">Todo bileşenine döndürür (*Todo.cshtml*):</span><span class="sxs-lookup"><span data-stu-id="d6ede-188">Return to the Todo component (*Todo.cshtml*):</span></span>

   * <span data-ttu-id="d6ede-189">Açıklamada içinde için bir alan eklemek bir `@functions` blok.</span><span class="sxs-lookup"><span data-stu-id="d6ede-189">Add a field for the todos in an `@functions` block.</span></span> <span data-ttu-id="d6ede-190">Todo bileşeni, yapılacaklar listesi durumunu korumak için bu alanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="d6ede-190">The Todo component uses this field to maintain the state of the todo list.</span></span>
   * <span data-ttu-id="d6ede-191">Sırasız liste biçimlendirme eklemek ve `foreach` her bir todo öğesi bir liste öğesi olarak işlenecek döngü.</span><span class="sxs-lookup"><span data-stu-id="d6ede-191">Add unordered list markup and a `foreach` loop to render each todo item as a list item.</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData4.cshtml?highlight=5-10,12-14)]

1. <span data-ttu-id="d6ede-192">Uygulama, açıklamada listeye eklemek için kullanıcı Arabirimi öğeleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d6ede-192">The app requires UI elements for adding todos to the list.</span></span> <span data-ttu-id="d6ede-193">Bir metin girişi ve listenin altındaki bir düğme ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d6ede-193">Add a text input and a button below the list:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData5.cshtml?highlight=12-13)]

1. <span data-ttu-id="d6ede-194">Yeniden oluşturun ve uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d6ede-194">Rebuild and run the app.</span></span> <span data-ttu-id="d6ede-195">Zaman **todo ekleyin** düğmesi seçilirse, hiçbir şey olmaz kadar düğmesi olay işleyicisi kablolu değildir çünkü.</span><span class="sxs-lookup"><span data-stu-id="d6ede-195">When the **Add todo** button is selected, nothing happens because an event handler isn't wired up to the button.</span></span>

1. <span data-ttu-id="d6ede-196">Ekleme bir `AddTodo` Todo bileşen ve düğme için tıkladığında kullanarak kayıt yöntemi `onclick` özniteliği:</span><span class="sxs-lookup"><span data-stu-id="d6ede-196">Add an `AddTodo` method to the Todo component and register it for button clicks using the `onclick` attribute:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData6.cshtml?highlight=2,7-10)]

   <span data-ttu-id="d6ede-197">`AddTodo` C# Yöntemi düğme seçildiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="d6ede-197">The `AddTodo` C# method is called when the button is selected.</span></span>

1. <span data-ttu-id="d6ede-198">Yeni todo öğesinin başlığını almak için ekleyin bir `newTodo` dize alanı ve değeri kullanarak metin olarak bağlama `bind` özniteliği:</span><span class="sxs-lookup"><span data-stu-id="d6ede-198">To get the title of the new todo item, add a `newTodo` string field and bind it to the value of the text input using the `bind` attribute:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData7.cshtml?highlight=2)]

   ```cshtml
   <input placeholder="Something todo" bind="@newTodo" />
   ```

1. <span data-ttu-id="d6ede-199">Güncelleştirme `AddTodo` ekleme yöntemi `TodoItem` listesine belirtilen başlığa sahip.</span><span class="sxs-lookup"><span data-stu-id="d6ede-199">Update the `AddTodo` method to add the `TodoItem` with the specified title to the list.</span></span> <span data-ttu-id="d6ede-200">Metin girişi değerini ayarlayarak Temizle `newTodo` boş bir dize:</span><span class="sxs-lookup"><span data-stu-id="d6ede-200">Clear the value of the text input by setting `newTodo` to an empty string:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData8.cshtml?highlight=19-26)]

1. <span data-ttu-id="d6ede-201">Yeniden oluşturun ve uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d6ede-201">Rebuild and run the app.</span></span> <span data-ttu-id="d6ede-202">Bazı açıklamada yeni kodu test etmek için yapılacaklar listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d6ede-202">Add some todos to the todo list to test the new code.</span></span>

1. <span data-ttu-id="d6ede-203">Her bir todo öğesi için başlık metnini düzenlenebilir hale getirilebilir ve onay kutusu tamamlanan öğeleri takip kullanıcı yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d6ede-203">The title text for each todo item can be made editable and a check box can help the user keep track of completed items.</span></span> <span data-ttu-id="d6ede-204">Her bir todo öğesi için bir onay kutusu giriş ekleyin ve değerini bağlama `IsDone` özelliği.</span><span class="sxs-lookup"><span data-stu-id="d6ede-204">Add a check box input for each todo item and bind its value to the `IsDone` property.</span></span> <span data-ttu-id="d6ede-205">Değişiklik `@todo.Title` için bir `<input>` bağlı öğe `@todo.Title`:</span><span class="sxs-lookup"><span data-stu-id="d6ede-205">Change `@todo.Title` to an `<input>` element bound to `@todo.Title`:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData9.cshtml?highlight=5-6)]

1. <span data-ttu-id="d6ede-206">Bu değerleri bağlı olduğunu doğrulamak için güncelleştirme `<h1>` tamamlanmamış todo öğelerini sayısını göstermek için başlık (`IsDone` olan `false`).</span><span class="sxs-lookup"><span data-stu-id="d6ede-206">To verify that these values are bound, update the `<h1>` header to show a count of the number of todo items that aren't complete (`IsDone` is `false`).</span></span>

   ```cshtml
   <h1>Todo (@todos.Count(todo => !todo.IsDone))</h1>
   ```

1. <span data-ttu-id="d6ede-207">Tamamlanmış Todo bileşeni (*Todo.cshtml*):</span><span class="sxs-lookup"><span data-stu-id="d6ede-207">The completed Todo component (*Todo.cshtml*):</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Todo.cshtml)]

1. <span data-ttu-id="d6ede-208">Yeniden oluşturun ve uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d6ede-208">Rebuild and run the app.</span></span> <span data-ttu-id="d6ede-209">Yeni kod test etmek için todo öğeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d6ede-209">Add todo items to test the new code.</span></span>

## <a name="publish-and-deploy-the-app"></a><span data-ttu-id="d6ede-210">Yayımlama ve uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="d6ede-210">Publish and deploy the app</span></span>

<span data-ttu-id="d6ede-211">Uygulamayı yayımlamak için bkz: <xref:host-and-deploy/razor-components/index#publish-the-app>.</span><span class="sxs-lookup"><span data-stu-id="d6ede-211">To publish the app, see <xref:host-and-deploy/razor-components/index#publish-the-app>.</span></span>
