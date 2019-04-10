---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: ASP.NET Web API'si - ASP.NET için Yardım sayfaları oluşturma 4.x
author: MikeWasson
description: Bu öğreticiyle kod ASP.NET'te ASP.NET Web API Yardım sayfaları oluşturma işlemini gösterir 4.x.
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: e3f6a9b8a6835b034a075d580cd9a33136969990
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59395023"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="8241a-103">ASP.NET Web API Yardım sayfaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="8241a-103">Creating Help Pages for ASP.NET Web API</span></span>

<span data-ttu-id="8241a-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8241a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="8241a-105">Bu öğreticiyle kod ASP.NET'te ASP.NET Web API Yardım sayfaları oluşturma işlemini gösterir 4.x.</span><span class="sxs-lookup"><span data-stu-id="8241a-105">This tutorial with code shows how to create help pages for ASP.NET Web API in ASP.NET 4.x.</span></span>

<span data-ttu-id="8241a-106">Web API'si oluşturma, böylece diğer geliştiriciler, API'nin nasıl çağrılacağını bilir, genellikle bir Yardım sayfasını oluşturmak kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="8241a-106">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="8241a-107">Tüm belgelerini el ile oluşturabilirsiniz, ancak mümkün olduğunca otomatik iyidir.</span><span class="sxs-lookup"><span data-stu-id="8241a-107">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span> <span data-ttu-id="8241a-108">Bu görevi kolaylaştırmak için ASP.NET Web API kitaplık çalışma zamanında otomatik olarak oluşturmak için Yardım sayfaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="8241a-108">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="8241a-109">API Yardım sayfaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="8241a-109">Creating API Help Pages</span></span>

<span data-ttu-id="8241a-110">Yükleme [ASP.NET ve Web Araçları 2012.2 güncelleştirme](https://go.microsoft.com/fwlink/?LinkId=282650).</span><span class="sxs-lookup"><span data-stu-id="8241a-110">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="8241a-111">Bu güncelleştirme ile Web API proje şablonunu yardım sayfalarına tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="8241a-111">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="8241a-112">Ardından, yeni bir ASP.NET MVC 4 projesi oluşturun ve Web API proje şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="8241a-112">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="8241a-113">Proje şablonu adlı bir örnek API denetleyicisi oluşturur `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="8241a-113">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="8241a-114">Şablon API Yardım sayfaları da oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8241a-114">The template also creates the API help pages.</span></span> <span data-ttu-id="8241a-115">Tüm kod dosyaları Yardım sayfası proje alanlarını klasöründe yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8241a-115">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="8241a-116">Uygulamayı çalıştırdığınızda giriş sayfasının API Yardım sayfası için bir bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="8241a-116">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="8241a-117">Giriş sayfasından, göreli yol/Help ' dir.</span><span class="sxs-lookup"><span data-stu-id="8241a-117">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="8241a-118">Bu bağlantı için bir API Özet sayfasında getirir.</span><span class="sxs-lookup"><span data-stu-id="8241a-118">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="8241a-119">Bu sayfa için MVC görünümü Areas/HelpPage/Views/Help/Index.cshtml içinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="8241a-119">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="8241a-120">Düzen, giriş, başlık, stillerini ve benzeri değiştirmek için bu sayfayı düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8241a-120">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="8241a-121">Ana sayfanın parçası, API, denetleyici tarafından gruplandırılmış bir tablodur.</span><span class="sxs-lookup"><span data-stu-id="8241a-121">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="8241a-122">Tablo girişleri kullanarak dinamik olarak oluşturulan **IApiExplorer** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="8241a-122">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="8241a-123">(Ben daha sonra bu arabirimi hakkında daha fazla konuşacağız.) Yeni bir API denetleyicisi eklerseniz, tablo, çalışma zamanında otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8241a-123">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="8241a-124">Göreli URI ve HTTP yöntemi "API" sütunu listeler.</span><span class="sxs-lookup"><span data-stu-id="8241a-124">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="8241a-125">"Description" sütunu, her API belgelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="8241a-125">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="8241a-126">Başlangıçta, yer tutucu metnini belgelerdir.</span><span class="sxs-lookup"><span data-stu-id="8241a-126">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="8241a-127">Sonraki bölümde, ı, belgeleri XML açıklamalarını ekleme göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="8241a-127">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="8241a-128">Her API, örnek istek ve yanıt gövdeleri dahil olmak üzere daha ayrıntılı bilgi içeren bir sayfa için bir bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="8241a-128">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="8241a-129">Mevcut bir projeyi yardım sayfalarına ekleme</span><span class="sxs-lookup"><span data-stu-id="8241a-129">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="8241a-130">NuGet Paket Yöneticisi'ni kullanarak yardım sayfalarına varolan bir Web API projesine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8241a-130">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="8241a-131">Bu seçenek, bir "Web API" şablonu değerinden farklı proje şablonundan başlattığınız yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="8241a-131">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="8241a-132">Gelen **Araçları** menüsünde **NuGet Paket Yöneticisi**ve ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="8241a-132">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="8241a-133">İçinde [Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) penceresinde, aşağıdaki komutlardan birini yazın:</span><span class="sxs-lookup"><span data-stu-id="8241a-133">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="8241a-134">İçin bir **C#** uygulama:</span><span class="sxs-lookup"><span data-stu-id="8241a-134">For a **C#** application:</span></span> `Install-Package Microsoft.AspNet.WebApi.HelpPage`

<span data-ttu-id="8241a-135">İçin bir **Visual Basic** uygulama:</span><span class="sxs-lookup"><span data-stu-id="8241a-135">For a **Visual Basic** application:</span></span> `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`

<span data-ttu-id="8241a-136">İki paket, bir C# ve Visual Basic için bir tane vardır.</span><span class="sxs-lookup"><span data-stu-id="8241a-136">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="8241a-137">Projenizi eşleşen bir kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8241a-137">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="8241a-138">Bu komut, gerekli bütünleştirilmiş kodları yükler ve MVC görünümleri (alanlar/HelpPage klasöründe bulunur) Yardım sayfaları için ekler.</span><span class="sxs-lookup"><span data-stu-id="8241a-138">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="8241a-139">Yardım sayfasına bir bağlantıyı el ile eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8241a-139">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="8241a-140">/ Help URI'dir.</span><span class="sxs-lookup"><span data-stu-id="8241a-140">The URI is /Help.</span></span> <span data-ttu-id="8241a-141">Razor Görünümü'nde bir bağlantı oluşturmak için aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8241a-141">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="8241a-142">Ayrıca, alanları kaydedilecek emin olun.</span><span class="sxs-lookup"><span data-stu-id="8241a-142">Also, make sure to register areas.</span></span> <span data-ttu-id="8241a-143">Global.asax dosyasında aşağıdaki kodu ekleyin **uygulama\_Başlat** orada değilse yöntemi:</span><span class="sxs-lookup"><span data-stu-id="8241a-143">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="8241a-144">API belgelerine ekleme</span><span class="sxs-lookup"><span data-stu-id="8241a-144">Adding API Documentation</span></span>

<span data-ttu-id="8241a-145">Varsayılan olarak, Yardım sayfaları, belgeler için yer tutucu dizeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="8241a-145">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="8241a-146">Kullanabileceğiniz [XML belgeleri yorumları](https://msdn.microsoft.com/library/b2s063f7.aspx) belgeleri oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="8241a-146">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="8241a-147">Bu özelliği etkinleştirmek için ' % s'dosyasını HelpPage/alanlar/uygulama açın\_Start/HelpPageConfig.cs ve aşağıdaki satırı açıklamadan çıkarın:</span><span class="sxs-lookup"><span data-stu-id="8241a-147">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="8241a-148">XML belgeleri artık etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8241a-148">Now enable XML documentation.</span></span> <span data-ttu-id="8241a-149">Çözüm Gezgini'nde projeye sağ tıklayıp seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="8241a-149">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="8241a-150">Seçin **derleme** sayfası.</span><span class="sxs-lookup"><span data-stu-id="8241a-150">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="8241a-151">Altında **çıkış**, kontrol **XML belge dosyası**.</span><span class="sxs-lookup"><span data-stu-id="8241a-151">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="8241a-152">Düzenleme kutusuna "uygulama\_Data/XmlDocument.xml".</span><span class="sxs-lookup"><span data-stu-id="8241a-152">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="8241a-153">Ardından, kodunu açmak `ValuesController` /Controllers/ValuesController.cs içinde tanımlanan API denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="8241a-153">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesController.cs.</span></span> <span data-ttu-id="8241a-154">Bazı belge açıklamaları için denetleyici yöntemleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8241a-154">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="8241a-155">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8241a-155">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="8241a-156">İpucu: Giriş işaretini satırın yöntem yukarıda getirin ve üç eğik çizgi yazın, Visual Studio XML öğeleri otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="8241a-156">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="8241a-157">Ardından, boşlukları doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8241a-157">Then you can fill in the blanks.</span></span>


<span data-ttu-id="8241a-158">Artık derleme ve uygulamayı yeniden çalıştırın ve Yardım sayfalarına gidin.</span><span class="sxs-lookup"><span data-stu-id="8241a-158">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="8241a-159">Belge dizeleri API tabloda görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8241a-159">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="8241a-160">Yardım sayfasına dizeleri çalışma zamanında XML dosyasından okur.</span><span class="sxs-lookup"><span data-stu-id="8241a-160">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="8241a-161">(Uygulama dağıttığınızda, XML dosyasını dağıtmak emin olun.)</span><span class="sxs-lookup"><span data-stu-id="8241a-161">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="8241a-162">Başlık altında</span><span class="sxs-lookup"><span data-stu-id="8241a-162">Under the Hood</span></span>

<span data-ttu-id="8241a-163">Üst kısmındaki yardım sayfalarına yerleşik **ApiExplorer** Web API çerçevesi parçası olan sınıf.</span><span class="sxs-lookup"><span data-stu-id="8241a-163">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="8241a-164">**ApiExplorer** sınıfı, bir Yardım sayfasını oluşturmak için ham madde sağlar.</span><span class="sxs-lookup"><span data-stu-id="8241a-164">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="8241a-165">Her API için **ApiExplorer** içeren bir **ApiDescription** API'sini açıklayan.</span><span class="sxs-lookup"><span data-stu-id="8241a-165">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="8241a-166">Bu amaç için bir "API" HTTP yöntemi ile göreli URL birleşimi tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="8241a-166">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="8241a-167">Örneğin, bazı ayrı API şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8241a-167">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="8241a-168">/Api/Products Al</span><span class="sxs-lookup"><span data-stu-id="8241a-168">GET /api/Products</span></span>
- <span data-ttu-id="8241a-169">Alma/API'si/ürünler / {id}</span><span class="sxs-lookup"><span data-stu-id="8241a-169">GET /api/Products/{id}</span></span>
- <span data-ttu-id="8241a-170">/ Api/ürünleri gönderin</span><span class="sxs-lookup"><span data-stu-id="8241a-170">POST /api/Products</span></span>

<span data-ttu-id="8241a-171">Bir denetleyici eylemi birden çok HTTP yöntemleri destekliyorsa **ApiExplorer** her yöntem farklı bir API olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="8241a-171">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="8241a-172">API'den gizlemek için **ApiExplorer**, ekleme **ApiExplorerSettings** öznitelik kümesi ve eylem *IgnoreApi* true.</span><span class="sxs-lookup"><span data-stu-id="8241a-172">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="8241a-173">Ayrıca, bu özniteliği denetleyiciye tüm denetleyicinin hariç tutmak için ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8241a-173">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="8241a-174">Belgeleri dizelerden ApiExplorer sınıfı alır **IDocumentationProvider** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="8241a-174">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="8241a-175">Daha önce bahsettiğim gibi Yardım sayfaları kitaplığı sağlayan bir **IDocumentationProvider** XML belgeleri dizelerden belgeleri alır.</span><span class="sxs-lookup"><span data-stu-id="8241a-175">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="8241a-176">Kod içinde /Areas/HelpPage/XmlDocumentationProvider.cs bulunur.</span><span class="sxs-lookup"><span data-stu-id="8241a-176">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="8241a-177">Belge başka bir kaynaktan yazarak kendi alabileceğiniz **IDocumentationProvider**.</span><span class="sxs-lookup"><span data-stu-id="8241a-177">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="8241a-178">Yukarı wire çağrısı **SetDocumentationProvider** genişletme yöntemi, tanımlanan **HelpPageConfigurationExtensions**</span><span class="sxs-lookup"><span data-stu-id="8241a-178">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="8241a-179">**ApiExplorer** otomatik olarak içine yapılan çağrılar **IDocumentationProvider** her bir API için belgeler dizelerini almak için arabirim.</span><span class="sxs-lookup"><span data-stu-id="8241a-179">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="8241a-180">Bu depolar **belgeleri** özelliği **ApiDescription** ve **ApiParameterDescription** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="8241a-180">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8241a-181">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="8241a-181">Next Steps</span></span>

<span data-ttu-id="8241a-182">Burada gösterilen yardım sayfalarına sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="8241a-182">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="8241a-183">Aslında, **ApiExplorer** Yardım sayfaları oluşturma için sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="8241a-183">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="8241a-184">Kullanıma hazır düşünmek başlamanızı sağlayacak bazı harika blog yazılarını yazılmış yao Huang Bağla:</span><span class="sxs-lookup"><span data-stu-id="8241a-184">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="8241a-185">ASP.NET Web API Yardım sayfası için basit bir Test istemcisi ekleme</span><span class="sxs-lookup"><span data-stu-id="8241a-185">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="8241a-186">ASP.NET Web API Yardım şirket içinde barındırılan hizmetleri üzerinde çalışma sayfası yapma</span><span class="sxs-lookup"><span data-stu-id="8241a-186">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="8241a-187">Yardım sayfası (veya istemci) ASP.NET Web API'si için tasarım zamanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8241a-187">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="8241a-188">Gelişmiş Yardım sayfası özelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8241a-188">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
