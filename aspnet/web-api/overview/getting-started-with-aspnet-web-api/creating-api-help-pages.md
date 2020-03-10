---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: ASP.NET Web API 'SI için yardım sayfaları oluşturma-ASP.NET 4. x
author: MikeWasson
description: Bu kod ile bu öğretici, ASP.NET 4. x içinde ASP.NET Web API 'SI için yardım sayfaları oluşturmayı gösterir.
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 8308dab8bd66aa8f5a3c5fb4133fc7a3df78f671
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556877"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="9fbdf-103">ASP.NET Web API 'SI için yardım sayfaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fbdf-103">Creating Help Pages for ASP.NET Web API</span></span>

<span data-ttu-id="9fbdf-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9fbdf-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="9fbdf-105">Bu kod ile bu öğretici, ASP.NET 4. x içinde ASP.NET Web API 'SI için yardım sayfaları oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-105">This tutorial with code shows how to create help pages for ASP.NET Web API in ASP.NET 4.x.</span></span>

<span data-ttu-id="9fbdf-106">Bir Web API 'SI oluşturduğunuzda, diğer geliştiricilerin API 'nizi nasıl çağırabileceğini bilmesi için, genellikle bir yardım sayfası oluşturmak yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-106">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="9fbdf-107">Tüm belgeleri el ile oluşturabilirsiniz, ancak mümkün olduğunca yeniden oluşturulması daha iyidir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-107">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span> <span data-ttu-id="9fbdf-108">Bu görevi daha kolay hale getirmek için ASP.NET Web API 'SI, çalışma zamanında otomatik olarak yardım sayfaları oluşturmak için bir kitaplık sağlar.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-108">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="9fbdf-109">API Yardım sayfaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fbdf-109">Creating API Help Pages</span></span>

<span data-ttu-id="9fbdf-110">[ASP.NET and Web Tools 2012,2 güncelleştirmesini](https://go.microsoft.com/fwlink/?LinkId=282650)yükler.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-110">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="9fbdf-111">Bu güncelleştirme yardım sayfalarını Web API 'SI proje şablonuyla tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-111">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="9fbdf-112">Sonra, yeni bir ASP.NET MVC 4 projesi oluşturun ve Web API 'SI proje şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-112">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="9fbdf-113">Proje şablonu, `ValuesController`adlı örnek bir API denetleyicisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-113">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="9fbdf-114">Şablon, API yardım sayfalarını da oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-114">The template also creates the API help pages.</span></span> <span data-ttu-id="9fbdf-115">Yardım sayfası için tüm kod dosyaları projenin Areas klasörüne yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-115">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="9fbdf-116">Uygulamayı çalıştırdığınızda, giriş sayfası API yardım sayfasına bir bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-116">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="9fbdf-117">Giriş sayfasından göreli yol/Help' dir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-117">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="9fbdf-118">Bu bağlantı sizi bir API özet sayfasına getirir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-118">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="9fbdf-119">Bu sayfanın MVC görünümü alanlarda/HelpPage/views/Help/Index. cshtml içinde tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-119">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="9fbdf-120">Bu sayfayı düzen, giriş, başlık, stiller vb. değiştirmek için düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-120">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="9fbdf-121">Sayfanın ana bölümü, denetleyiciye göre gruplandırılan bir API tablosudur.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-121">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="9fbdf-122">Tablo girdileri, **IApiExplorer** arabirimi kullanılarak dinamik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-122">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="9fbdf-123">(Bu arabirim hakkında daha sonra daha fazla konuşacak.) Yeni bir API denetleyicisi eklerseniz, tablo çalışma zamanında otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-123">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="9fbdf-124">"API" sütunu, HTTP yöntemini ve göreli URI 'yi listeler.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-124">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="9fbdf-125">"Açıklama" sütunu her API için belgeler içerir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-125">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="9fbdf-126">Başlangıçta, belgeler yalnızca yer tutucu metindir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-126">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="9fbdf-127">Sonraki bölümde, XML açıklamalarından nasıl belge ekleneceğini göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-127">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="9fbdf-128">Her API, örnek istek ve yanıt gövdeleri dahil olmak üzere daha ayrıntılı bilgiler içeren bir sayfanın bağlantısını içerir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-128">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="9fbdf-129">Mevcut bir projeye yardım sayfaları ekleme</span><span class="sxs-lookup"><span data-stu-id="9fbdf-129">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="9fbdf-130">NuGet Paket Yöneticisi 'Ni kullanarak var olan bir Web API projesine yardım sayfaları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-130">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="9fbdf-131">Bu seçenek, "Web API" şablonundan farklı bir proje şablonundan başlayabilmeniz için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-131">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="9fbdf-132">**Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni seçin ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-132">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="9fbdf-133">[Paket Yöneticisi konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) penceresinde, aşağıdaki komutlardan birini yazın:</span><span class="sxs-lookup"><span data-stu-id="9fbdf-133">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="9fbdf-134">Bir **C#** uygulama için: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="9fbdf-134">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="9fbdf-135">**Visual Basic** bir uygulama için: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="9fbdf-135">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="9fbdf-136">Biri için C# bir diğeri Visual Basic olmak üzere iki paket vardır.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-136">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="9fbdf-137">Projenizle eşleşen birini kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-137">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="9fbdf-138">Bu komut, gerekli derlemeleri yükleyip yardım sayfaları (Areas/HelpPage klasöründe bulunur) için MVC görünümlerini ekler.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-138">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="9fbdf-139">Yardım sayfasına el ile bir bağlantı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-139">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="9fbdf-140">URI,/Help.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-140">The URI is /Help.</span></span> <span data-ttu-id="9fbdf-141">Razor görünümünde bir bağlantı oluşturmak için aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9fbdf-141">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="9fbdf-142">Ayrıca, alanların kaydettirildiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-142">Also, make sure to register areas.</span></span> <span data-ttu-id="9fbdf-143">Global. asax dosyasında, zaten mevcut değilse, **uygulama\_start** yöntemine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9fbdf-143">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="9fbdf-144">API belgeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="9fbdf-144">Adding API Documentation</span></span>

<span data-ttu-id="9fbdf-145">Varsayılan olarak, yardım sayfalarında belgeler için yer tutucu dizeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-145">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="9fbdf-146">Belgeleri oluşturmak için [XML belge açıklamalarını](https://msdn.microsoft.com/library/b2s063f7.aspx) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-146">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="9fbdf-147">Bu özelliği etkinleştirmek için, Start/HelpPageConfig. cs\_dosya bölgelerini/HelpPage/App açın ve aşağıdaki satırın açıklamasını kaldırın:</span><span class="sxs-lookup"><span data-stu-id="9fbdf-147">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="9fbdf-148">Şimdi XML belgelerini etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-148">Now enable XML documentation.</span></span> <span data-ttu-id="9fbdf-149">Çözüm Gezgini, projeye sağ tıklayın ve **Özellikler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-149">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="9fbdf-150">**Yapı** sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-150">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="9fbdf-151">**Çıkış**' ın altında, **XML belge dosyasını**denetleyin.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-151">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="9fbdf-152">Düzenleme kutusuna "App\_Data/XmlDocument. xml" yazın.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-152">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="9fbdf-153">Daha sonra,/Controllers/valuescontroller.exe. csv dosyasında tanımlanan `ValuesController` API denetleyicisi için kodu açın.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-153">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesController.cs.</span></span> <span data-ttu-id="9fbdf-154">Denetleyici yöntemlerine bazı belge açıklamalarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-154">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="9fbdf-155">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9fbdf-155">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="9fbdf-156">İpucu: giriş işaretini yöntemin üzerindeki satıra konumlandırır ve üç eğik çizgi yazarsanız, Visual Studio otomatik olarak XML öğelerini ekler.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-156">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="9fbdf-157">Daha sonra boşlukları doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-157">Then you can fill in the blanks.</span></span>

<span data-ttu-id="9fbdf-158">Şimdi uygulamayı yeniden derleyin ve çalıştırın ve yardım sayfalarına gidin.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-158">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="9fbdf-159">Belge dizeleri API tablosunda görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-159">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="9fbdf-160">Yardım sayfası, XML dosyasındaki dizeleri çalışma zamanında okur.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-160">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="9fbdf-161">(Uygulamayı dağıtırken, XML dosyasını dağıttığınızdan emin olun.)</span><span class="sxs-lookup"><span data-stu-id="9fbdf-161">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="9fbdf-162">Üzerinde</span><span class="sxs-lookup"><span data-stu-id="9fbdf-162">Under the Hood</span></span>

<span data-ttu-id="9fbdf-163">Yardım sayfaları, Web API çerçevesinin bir parçası olan **Apiexplorer** sınıfının üzerine kurulmuştur.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-163">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="9fbdf-164">**Apiexplorer** sınıfı, yardım sayfası oluşturmak için ham malzeme sağlar.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-164">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="9fbdf-165">Her API için **Apiexplorer** , API 'yi açıklayan bir **apidescription** içerir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-165">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="9fbdf-166">Bu amaçla, bir "API" HTTP yönteminin ve göreli URI 'nin birleşimi olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-166">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="9fbdf-167">Örneğin, bazı farklı API 'Ler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9fbdf-167">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="9fbdf-168">/Api/Products al</span><span class="sxs-lookup"><span data-stu-id="9fbdf-168">GET /api/Products</span></span>
- <span data-ttu-id="9fbdf-169">/Api/Products/{ID} Al</span><span class="sxs-lookup"><span data-stu-id="9fbdf-169">GET /api/Products/{id}</span></span>
- <span data-ttu-id="9fbdf-170">GÖNDERI/api/Products</span><span class="sxs-lookup"><span data-stu-id="9fbdf-170">POST /api/Products</span></span>

<span data-ttu-id="9fbdf-171">Bir denetleyici eylemi birden çok HTTP yöntemini destekliyorsa, **Apiexplorer** her bir yöntemi ayrı bir API olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-171">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="9fbdf-172">**Apiexplorer**'DAN bir API 'yi gizlemek için, eyleme **Apiexplorersettings** özniteliğini ekleyin ve *ıgnoreapı* değerini doğru olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-172">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="9fbdf-173">Denetleyicinin tamamını hariç tutmak için bu özniteliği denetleyiciye de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-173">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="9fbdf-174">ApiExplorer sınıfı, **ıbelgelertationprovider** arabiriminden belge dizelerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-174">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="9fbdf-175">Daha önce gördüğünüz gibi yardım sayfaları kitaplığı, XML belge dizelerinden belgeler alan bir **ıbelgelertationprovider** sağlar.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-175">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="9fbdf-176">Kod/Areas/helppage/xmlbelgetationprovider.exe konumunda bulunur.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-176">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="9fbdf-177">Kendi **ıbelgeleribelgelerinizi**yazarak başka bir kaynaktan belge alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-177">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="9fbdf-178">Bunu yapmak için, **Helppageconfigurationextensions** Içinde tanımlanan **Setbelgetationprovider** uzantı yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-178">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="9fbdf-179">**Apiexplorer** , her API için belge dizelerini almak üzere otomatik olarak **ıbelgelertationprovider** arabirimine çağırır.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-179">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="9fbdf-180">Bunları **Apidescription** ve **apiparameterdescription** nesnelerinin **documentation** özelliğinde depolar.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-180">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fbdf-181">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="9fbdf-181">Next Steps</span></span>

<span data-ttu-id="9fbdf-182">Burada gösterilen yardım sayfalarıyla sınırlı değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-182">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="9fbdf-183">Aslında, **Apiexplorer** yardım sayfaları oluşturmak için sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="9fbdf-183">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="9fbdf-184">Yao Huang Lin, daha fazla bilgi edinmek için harika blog gönderileri yazmıştır:</span><span class="sxs-lookup"><span data-stu-id="9fbdf-184">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="9fbdf-185">ASP.NET Web API 'SI yardım sayfasına basit bir test Istemcisi ekleme</span><span class="sxs-lookup"><span data-stu-id="9fbdf-185">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="9fbdf-186">ASP.NET Web API Yardım sayfası, şirket içinde barındırılan hizmetler üzerinde çalışır hale getirme</span><span class="sxs-lookup"><span data-stu-id="9fbdf-186">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="9fbdf-187">ASP.NET Web API 'SI için tasarım zamanı oluşturma Yardım sayfası (veya istemcisi)</span><span class="sxs-lookup"><span data-stu-id="9fbdf-187">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="9fbdf-188">Gelişmiş yardım sayfası özelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="9fbdf-188">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
