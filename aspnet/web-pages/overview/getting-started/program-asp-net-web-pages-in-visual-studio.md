---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Visual Studio kullanarak ASP.NET Web Pages (Razor) programlama | Microsoft Docs
author: Rick-Anderson
description: Bu ekte, Razor söz dizimi ile Web sayfalarını ASP.NET programlamak için Visual Studio 2010 veya Visual Web Developer 2010 Express 'i nasıl kullanabileceğiniz açıklanır.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633513"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="3f707-103">Visual Studio kullanarak ASP.NET Web Pages (Razor) programlama</span><span class="sxs-lookup"><span data-stu-id="3f707-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="3f707-104">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="3f707-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3f707-105">Bu makalede, ASP.NET Web Pages (Razor) Web sitelerini programlamak için Visual Studio veya Visual Web Developer Express 'i nasıl kullanabileceğiniz açıklanır.</span><span class="sxs-lookup"><span data-stu-id="3f707-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="3f707-106">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="3f707-106">What you'll learn</span></span>
>
> - <span data-ttu-id="3f707-107">Visual Studio sürümünüzde ASP.NET Web sayfalarıyla çalışmak için (varsa) yüklemeniz gerekenler.</span><span class="sxs-lookup"><span data-stu-id="3f707-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="3f707-108">Visual Web Developer 2010 Express 'e ASP.NET Web sayfaları için destek ekleme.</span><span class="sxs-lookup"><span data-stu-id="3f707-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="3f707-109">IntelliSense ve hata ayıklayıcı dahil olmak üzere ASP.NET Razor sayfalarıyla çalışmak için Visual Studio 'daki özellikleri kullanma.</span><span class="sxs-lookup"><span data-stu-id="3f707-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3f707-110">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="3f707-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="3f707-111">ASP.NET Web sayfaları (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="3f707-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="3f707-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3f707-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="3f707-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="3f707-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="3f707-114">Bu öğretici Ayrıca ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010 ve WebMatrix 2 ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3f707-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="3f707-115">Razor söz dizimi Web sayfalarını WebMatrix veya diğer birçok kod Düzenleyicisi kullanarak ASP.NET programlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f707-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="3f707-116">Ayrıca, çok sayıda uygulama (yalnızca Web siteleri değil) oluşturmak için güçlü bir araç kümesi sağlayan, tam özellikli bir tümleşik geliştirme ortamı (IDE) olan Microsoft Visual Studio de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f707-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="3f707-117">ASP.NET Razor sayfalarıyla çalışmak için [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)' i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f707-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="3f707-118">Visual Studio 'nun ASP.NET Razor Web sayfalarıyla programlama için sağladığı, özellikle yararlı olan iki özellik şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3f707-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="3f707-119">*IntelliSense*.</span><span class="sxs-lookup"><span data-stu-id="3f707-119">*IntelliSense*.</span></span> <span data-ttu-id="3f707-120">Visual Studio 'da yerleşik olarak bulunan IntelliSense özelliği, WebMatrix 'teki IntelliSense 'ten daha kapsamlıdır.</span><span class="sxs-lookup"><span data-stu-id="3f707-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="3f707-121">*Hata ayıklayıcı*.</span><span class="sxs-lookup"><span data-stu-id="3f707-121">*Debugger*.</span></span> <span data-ttu-id="3f707-122">Hata ayıklayıcı, çalışırken bir programı durdurup, değişkenleri inceleyerek ve satıra göre kod satırı üzerinden adımlayarak kodunuzun sorunlarını gidermenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3f707-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="3f707-123">Visual Studio 'Yu ASP.NET Web sayfalarının farklı sürümleriyle kullanma</span><span class="sxs-lookup"><span data-stu-id="3f707-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="3f707-124">Visual Studio 2017 ' de ASP.NET Web uygulamaları geliştirmek için, **ASP.net ve Web geliştirme** iş yükünü yüklemek.</span><span class="sxs-lookup"><span data-stu-id="3f707-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="3f707-125">Visual Studio 2012 ve Visual Studio 2013 ASP.NET Web Pages desteğini içerir.</span><span class="sxs-lookup"><span data-stu-id="3f707-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="3f707-126">(ASP.NET Web sayfalarını desteklemek için gereken paketler, Visual Studio 'Yu yüklediğinizde yüklenir.)</span><span class="sxs-lookup"><span data-stu-id="3f707-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="3f707-127">Visual Studio 2010, ASP.NET Web sayfaları için varsayılan olarak desteği içermez.</span><span class="sxs-lookup"><span data-stu-id="3f707-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="3f707-128">Visual Studio 2010 ile ASP.NET Web sayfalarını kullanmak için ASP.NET MVC paketini yüklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="3f707-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="3f707-129">ASP.NET Web sayfaları 2 ' yi almak için ASP.NET MVC 4 ' ü yüklersiniz.</span><span class="sxs-lookup"><span data-stu-id="3f707-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="3f707-130">Aşağıdaki tabloda, Visual Studio 'nun farklı sürümlerindeki ASP.NET Web sayfalarına yönelik destek özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="3f707-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="3f707-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="3f707-131">Visual Studio 2010</span></span> | <span data-ttu-id="3f707-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="3f707-132">Visual Studio 2012</span></span> | <span data-ttu-id="3f707-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3f707-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3f707-134">**ASP.NET Web sayfaları 2**</span><span class="sxs-lookup"><span data-stu-id="3f707-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="3f707-135">ASP.NET MVC 4 ' ü yükler</span><span class="sxs-lookup"><span data-stu-id="3f707-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="3f707-136">Verilen</span><span class="sxs-lookup"><span data-stu-id="3f707-136">(Included)</span></span> | <span data-ttu-id="3f707-137">Verilen</span><span class="sxs-lookup"><span data-stu-id="3f707-137">(Included)</span></span> |
| <span data-ttu-id="3f707-138">**ASP.NET Web sayfaları 3**</span><span class="sxs-lookup"><span data-stu-id="3f707-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="3f707-139">NuGet aracılığıyla ASP.NET Web Pages 3 ' e güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="3f707-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="3f707-140">Verilen</span><span class="sxs-lookup"><span data-stu-id="3f707-140">(Included)</span></span> |

<span data-ttu-id="3f707-141">Visual Studio 2010 ile çalışmak için bkz. [Visual studio 2010 ' de ASP.NET Web Pages Için destek yükleme](#vs2010support).</span><span class="sxs-lookup"><span data-stu-id="3f707-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="3f707-142">WebMatrix 'ten Visual Studio 'Yu başlatma</span><span class="sxs-lookup"><span data-stu-id="3f707-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="3f707-143">WebMatrix 'te bir proje başlattıysanız ve Visual Studio 'ya geçiş yapmak istiyorsanız, WebMatrix projeyi Visual Studio 'da kolayca açmak için bir düğme sağlar.</span><span class="sxs-lookup"><span data-stu-id="3f707-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="3f707-144">Bu düğmenin etkinleştirilmesi için bilgisayarınızda Visual Studio yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3f707-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="3f707-145">Aşağıdaki görüntüde WebMatrix içindeki düğme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3f707-145">The following image shows the button in WebMatrix.</span></span>

![Visual Studio 'Yu Başlat](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="3f707-147">Düğmeye tıkladığınızda, proje Visual Studio 'da açılır.</span><span class="sxs-lookup"><span data-stu-id="3f707-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="3f707-148">Herhangi bir sorun olmadan WebMatrix ve Visual Studio arasında geri ve ileri geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f707-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="3f707-149">Diğer ortamda herhangi bir dosya değiştiyse ve en son değişiklikleri almak için yeniden yüklenmesi gerekiyorsa size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="3f707-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="3f707-150">Visual Studio 'da ASP.NET Razor sitesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3f707-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="3f707-151">Visual Studio 'da bir ASP.NET Razor Web sitesi oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="3f707-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="3f707-152">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="3f707-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="3f707-153">**Dosya** menüsünde **Yeni Web sitesi**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f707-153">In the **File** menu, click **New Web Site**.</span></span>

    ![Yeni Web sitesi oluştur](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="3f707-155">**Yeni Web sitesi** iletişim kutusunda kullanılacak dili seçin (görsel C# veya Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="3f707-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="3f707-156">**ASP.NET Web sitesi (Razor)** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="3f707-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![Razor sitesi](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="3f707-158">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f707-158">Click **OK**.</span></span>

<span data-ttu-id="3f707-159">Yeni projeniz var ve kullanmaya başlamanıza yardımcı olacak bazı varsayılan Web sayfalarıyla doldurulmuştur.</span><span class="sxs-lookup"><span data-stu-id="3f707-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="3f707-160">IntelliSense Kullanma</span><span class="sxs-lookup"><span data-stu-id="3f707-160">Using IntelliSense</span></span>

<span data-ttu-id="3f707-161">Artık bir site oluşturduğunuza göre, IntelliSense 'in Visual Studio 'da nasıl çalıştığını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f707-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="3f707-162">Yeni oluşturduğunuz Web sitesinde *default. cshtml* sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="3f707-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="3f707-163">Sayfadaki `<h3>` etiketlerden sonra, `@ServerInfo.` (nokta dahil) yazın.</span><span class="sxs-lookup"><span data-stu-id="3f707-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="3f707-164">IntelliSense 'in bir açılan listede `ServerInfo` Yardımcısı için kullanılabilir yöntemleri nasıl görüntüleyeceği hakkında dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="3f707-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![IntelliSense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="3f707-166">Listeden `GetHtml` yöntemi seçin ve ardından ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="3f707-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="3f707-167">IntelliSense, yöntemi otomatik olarak doldurur.</span><span class="sxs-lookup"><span data-stu-id="3f707-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="3f707-168">(İçinde C#herhangi bir yöntemde olduğu gibi, yönteminden sonra `()` karakterler eklemeniz gerekir.) `GetHtml` yöntemi için tamamlanan kod aşağıdaki örneğe benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="3f707-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="3f707-169">Sayfayı çalıştırmak için CTRL + F5 tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="3f707-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="3f707-170">Bu, sayfanın bir tarayıcıda görüntülenmesiyle benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="3f707-170">This is what the page looks like when displayed in a browser:</span></span>

    ![tarayıcıda varsayılan sayfa](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="3f707-172">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="3f707-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="3f707-173">Hata ayıklayıcıyı kullanma</span><span class="sxs-lookup"><span data-stu-id="3f707-173">Using the Debugger</span></span>

1. <span data-ttu-id="3f707-174">*Default. cshtml* sayfasının en üstünde, `Page.Title`ile başlayan satırdan sonra aşağıdaki kod satırını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3f707-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="3f707-175">Düzenleyicinin solundaki düzenleyicinin gri kenar boşluğunda, bir *kesme noktası*eklemek için bu yeni satıra ileri ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f707-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="3f707-176">Kesme noktası, hata ayıklayıcıya programın bu noktada çalışmayı durdurmasını, böylece neler olduğunu görmeniz gerektiğini belirten bir işaretçidir.</span><span class="sxs-lookup"><span data-stu-id="3f707-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![Kesme noktası ayarla](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="3f707-178">`ServerInfo.GetHtml` yöntemine yapılan çağrıyı kaldırın ve onun yerine `@myTime` değişkenine bir çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3f707-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="3f707-179">Bu çağrı, yeni kod satırıyla döndürülen geçerli saat değerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3f707-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="3f707-180">Hata ayıklayıcıda sayfayı çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="3f707-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="3f707-181">Sayfa, ayarladığınız kesme noktasında durmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3f707-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="3f707-182">Aşağıdaki görüntüde, sayfanın kesme noktası (sarı) ile düzenleyicide nasıl göründüğü gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3f707-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![hata ayıklama kesme noktası](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="3f707-184">Sonraki kod satırını çalıştırmak için hata ayıklama araç çubuğunda **adımla** düğmesine (veya F11 tuşuna basın) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f707-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="3f707-185">Bu düğmeye tıkladığınızda, yürütmeyi bir sonraki kod satırına ilerletin.</span><span class="sxs-lookup"><span data-stu-id="3f707-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![Adımla düğmesi](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="3f707-187">`myTime` değişkenin değerini, fare işaretçinizi bunun üzerinde tutarak veya **Yereller** ve **çağrı yığını** pencerelerinde görünen değerleri inceleyerek inceleyin.</span><span class="sxs-lookup"><span data-stu-id="3f707-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="3f707-188">Visual Studio, değişkenin değerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3f707-188">Visual Studio display the value of the variable.</span></span>

    ![saat değerini göster](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="3f707-190">Değişkeni incelemeyi ve kod içinde adımlamayı tamamladıktan sonra, her satırda durmadan sayfayı çalıştırmaya devam etmek için F5 'e basın.</span><span class="sxs-lookup"><span data-stu-id="3f707-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="3f707-191">Tüm kodda adımlamayı bitirdiğinizde tarayıcı sayfayı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3f707-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="3f707-192">Hata ayıklayıcı hakkında daha fazla bilgi edinmek ve Visual Studio 'da kod hata ayıklama hakkında daha fazla bilgi için bkz. [Izlenecek yol: Visual Web Developer 'Da Web sayfalarında hata ayıklama](https://msdn.microsoft.com/library/z9e7w6cs.aspx)</span><span class="sxs-lookup"><span data-stu-id="3f707-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="3f707-193">Visual Studio ile ASP.NET MVC projelerinde Razor kullanma</span><span class="sxs-lookup"><span data-stu-id="3f707-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="3f707-194">Razor söz dizimi Ayrıca, ASP.NET MVC projelerinde kapsamlı olarak da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3f707-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="3f707-195">MVC, dinamik Web siteleri oluşturmaya yönelik güçlü ve desenlere dayalı bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="3f707-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="3f707-196">ASP.NET Web sayfaları sitenizin bakımı zor hale gelirse, bunu bir ASP.NET MVC uygulamasına dönüştürmeyi düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f707-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="3f707-197">MVC uygulaması oluşturma örneği için bkz. [ASP.NET MVC 5 Ile çalışmaya](../../../mvc/overview/getting-started/introduction/getting-started.md)başlama.</span><span class="sxs-lookup"><span data-stu-id="3f707-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="3f707-198">Visual Studio 2010 ' de ASP.NET Web sayfaları için destek yükleme</span><span class="sxs-lookup"><span data-stu-id="3f707-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="3f707-199">Bu bölüm Visual Studio için Visual Web Developer Express 2010 ve ASP.NET Web Pages araçları 'nın nasıl yükleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="3f707-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="3f707-200">Web Platformu Yükleyicisi yoksa, aşağıdaki URL 'den indirin:</span><span class="sxs-lookup"><span data-stu-id="3f707-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="3f707-201">Web Platformu Yükleyicisi 'ni çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f707-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="3f707-202">**Ürünler** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f707-202">Click the **Products** tab.</span></span>

    ![WebPI ürünleri sekmesi](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="3f707-204">**ASP.NET MVC 4** ' ü arayın (ASP.NET Web sayfaları 2 için) ve ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f707-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="3f707-205">Bu ürünler, ASP.NET Razor Web siteleri oluşturmak için Visual Studio araçları içerir.</span><span class="sxs-lookup"><span data-stu-id="3f707-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPI yüklemesi seçenekleri](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="3f707-207">Yüklemeyi **gerçekleştirmek için yükleme** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f707-207">Click **Install** to complete the installation.</span></span>
