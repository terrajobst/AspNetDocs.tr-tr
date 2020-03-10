---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: ASP.NET MVC 'de sayfa denetçisini kullanma | Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 ' deki sayfa denetçisi tümleşik tarayıcıyla bir Web geliştirme aracıdır. Tümleşik tarayıcıda ve sayfa denetçisi ı ' nde herhangi bir öğe seçin...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5da3e142c52a770f59222c21d9f9a53cbbdbf498
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538019"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a><span data-ttu-id="8bc07-104">ASP.NET MVC'de Sayfa Denetçisini Kullanma</span><span class="sxs-lookup"><span data-stu-id="8bc07-104">Using Page Inspector in ASP.NET MVC</span></span>

<span data-ttu-id="8bc07-105">, Tim Ammann tarafından</span><span class="sxs-lookup"><span data-stu-id="8bc07-105">by Tim Ammann</span></span>

> <span data-ttu-id="8bc07-106">Visual Studio 2012 ' deki sayfa denetçisi tümleşik tarayıcıyla bir Web geliştirme aracıdır.</span><span class="sxs-lookup"><span data-stu-id="8bc07-106">Page Inspector in Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="8bc07-107">Tümleşik tarayıcıda herhangi bir öğeyi seçin ve sayfa denetçisi öğenin kaynağını ve CSS 'sini anında vurgular.</span><span class="sxs-lookup"><span data-stu-id="8bc07-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="8bc07-108">Herhangi bir MVC görünümüne gözatabilir, işlenmiş biçimlendirmenin kaynaklarını hızlıca bulabilir ve Visual Studio ortamında doğrudan tarayıcı araçları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-108">You can browse any MVC view, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> [<span data-ttu-id="8bc07-109">Videoyu izleyin</span><span class="sxs-lookup"><span data-stu-id="8bc07-109">Watch the Video</span></span>](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> <span data-ttu-id="8bc07-110">Bu öğreticide Inceleme modunun nasıl etkinleştirileceği gösterilir ve sonra Web projenizde biçimlendirmeyi ve CSS 'yi hızlıca bulun ve düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-110">This tutorial shows how to enable Inspection Mode, and then quickly locate and edit markup and CSS within your web project.</span></span> <span data-ttu-id="8bc07-111">Öğretici bir MVC projesi kullanır, ancak [Web Forms](https://go.microsoft.com/?linkid=9802001) ve diğer ASP.NET uygulamaları Için sayfa denetçisi de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-111">The tutorial uses an MVC Project, but you can also use Page Inspector for [Web Forms](https://go.microsoft.com/?linkid=9802001) and other ASP.NET applications.</span></span>
> 
> <span data-ttu-id="8bc07-112">Öğreticide aşağıdaki bölümler bulunur:</span><span class="sxs-lookup"><span data-stu-id="8bc07-112">The tutorial has the following sections:</span></span>
> 
> - [<span data-ttu-id="8bc07-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8bc07-113">Prerequisites</span></span>](#_1_prerequisites)
> - [<span data-ttu-id="8bc07-114">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="8bc07-114">Create a Web Application</span></span>](#_2_creating_a)
> - [<span data-ttu-id="8bc07-115">Bir görünüme gitmek için sayfa denetçisini kullanma</span><span class="sxs-lookup"><span data-stu-id="8bc07-115">Use Page Inspector to Browse to a View</span></span>](#_3_using_page)
> - [<span data-ttu-id="8bc07-116">Inceleme modunu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="8bc07-116">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> - [<span data-ttu-id="8bc07-117">Işaretlemede değişiklik yapmak için sayfa denetçisini kullanın</span><span class="sxs-lookup"><span data-stu-id="8bc07-117">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> - [<span data-ttu-id="8bc07-118">İnceleme modu ve HTML penceresi</span><span class="sxs-lookup"><span data-stu-id="8bc07-118">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> - [<span data-ttu-id="8bc07-119">Stiller penceresinde CSS değişikliklerinin önizlemesi</span><span class="sxs-lookup"><span data-stu-id="8bc07-119">Preview CSS Changes in the Styles window</span></span>](#_7_previewing_css)
> - [<span data-ttu-id="8bc07-120">CSS otomatik eşitleme</span><span class="sxs-lookup"><span data-stu-id="8bc07-120">CSS Auto Sync</span></span>](#css_auto_sync)
> - [<span data-ttu-id="8bc07-121">CSS renk seçiciyi kullanma</span><span class="sxs-lookup"><span data-stu-id="8bc07-121">Using the CSS Color Picker</span></span>](#css_color_picker)
> - [<span data-ttu-id="8bc07-122">Dinamik sayfa öğelerini JavaScript 'e eşleme</span><span class="sxs-lookup"><span data-stu-id="8bc07-122">Mapping Dynamic Page Elements to JavaScript</span></span>](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="8bc07-123">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8bc07-123">Prerequisites</span></span>

- <span data-ttu-id="8bc07-124">Web için [Visual Studio 2012](https://www.microsoft.com/visualstudio/11) veya [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span><span class="sxs-lookup"><span data-stu-id="8bc07-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="8bc07-125">Sayfa denetçisinin en son sürümünü almak için, .NET 2,0 için Microsoft Azure SDK 'sını yüklemek üzere [Web Platformu Yükleyicisi](https://go.microsoft.com/fwlink/?LinkId=255386) ' ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-125">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Windows Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="8bc07-126">Sayfa denetçisi Microsoft Web Geliştirici Araçları ile paketlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-126">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="8bc07-127">En son sürüm 1,3 ' dir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-127">The latest version is 1.3.</span></span> <span data-ttu-id="8bc07-128">Sahip olduğunuz sürümü denetlemek için, Visual Studio 'Yu çalıştırın ve **Yardım** menüsünden **Microsoft Visual Studio hakkında** ' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-128">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="8bc07-129">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="8bc07-129">Create a Web Application</span></span>

<span data-ttu-id="8bc07-130">İlk olarak, ile sayfa denetçisi kullanacağınız bir Web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8bc07-130">First, create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="8bc07-131">Visual Studio 'da **dosya** &gt; **Yeni proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-131">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="8bc07-132">Sol tarafta, **C#görsel**' i genişletin, **Web**' i seçin ve **ASP.net MVC4 Web uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-132">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span>

![Yeni ASP.NET MVC uygulaması](using-page-inspector-in-aspnet-mvc/_static/image2.png)

<span data-ttu-id="8bc07-134">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-134">Click **OK**.</span></span>

<span data-ttu-id="8bc07-135">**Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **Internet uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-135">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="8bc07-136">**Razor** 'yi varsayılan görünüm altyapısı olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-136">Leave **Razor** as the default view engine.</span></span>

![Yeni ASP.NET MVC projesi-Internet uygulaması](using-page-inspector-in-aspnet-mvc/_static/image4.png)

<span data-ttu-id="8bc07-138">Uygulama **kaynak** görünümü ' nde açılır.</span><span class="sxs-lookup"><span data-stu-id="8bc07-138">The application opens in **Source** view.</span></span>

![Kaynak görünümünde yeni ASP.NET MVC uygulaması](using-page-inspector-in-aspnet-mvc/_static/image6.png)

<span data-ttu-id="8bc07-140">Artık birlikte çalışmak üzere bir uygulamanız olduğuna göre, sayfayı incelemek ve değiştirmek için sayfa denetçisi ' ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-140">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a><span data-ttu-id="8bc07-141">Bir görünüme gitmek için sayfa denetçisini kullanma</span><span class="sxs-lookup"><span data-stu-id="8bc07-141">Use Page Inspector to Browse to a View</span></span>

<span data-ttu-id="8bc07-142">Visual Studio 2012 ' de, projenizdeki herhangi bir görünüme sağ tıklayabilir, **sayfa denetçisinde görünüm**' ü seçtiğinizde, sayfa denetçisi bu yolu gösterir ve sayfayı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8bc07-142">In Visual Studio 2012, you can right-click any view in your project, select **View in Page Inspector**, and Page Inspector will figure out the route and display the page.</span></span>

<span data-ttu-id="8bc07-143">**Çözüm Gezgini**' de, **Görünümler** klasörünü ve ardından **giriş** klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-143">In **Solution Explorer**, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="8bc07-144">Index. cshtml dosyasına sağ tıklayın ve **sayfa denetçisinde görüntüle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-144">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

![Sayfa denetçisinde Index. cshtml 'yi görüntüle](using-page-inspector-in-aspnet-mvc/_static/image8.png)

<span data-ttu-id="8bc07-146">Varsayılan olarak, sayfa denetçisi Visual Studio ortamının sol tarafında bir pencere olarak Yuvalandırılmış olur.</span><span class="sxs-lookup"><span data-stu-id="8bc07-146">By default, Page Inspector is docked as a window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="8bc07-147">İsterseniz, başka bir yere sabitleyebilir veya pencereyi serbest bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-147">If you prefer, you can dock it elsewhere, or undock the window.</span></span> <span data-ttu-id="8bc07-148">Bkz. [nasıl yapılır: pencereleri düzenleme ve yerleştirme](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span><span class="sxs-lookup"><span data-stu-id="8bc07-148">See [How to: Arrange and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span></span>

<span data-ttu-id="8bc07-149">Sayfa denetçisi penceresinin üst bölmesi, geçerli sayfayı bir tarayıcı penceresinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-149">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="8bc07-150">Alt bölmede, sayfanın farklı yönlerini incelemenize olanak tanıyan bazı sekmeler ile birlikte HTML biçimlendirmesinde sayfa gösterilir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-150">The bottom pane shows the page in HTML markup, along with some tabs that let you inspect different aspects of the page.</span></span> <span data-ttu-id="8bc07-151">Alt bölme, Internet Explorer 'daki [F12 geliştirici araçları](https://msdn.microsoft.com/ie/aa740478) benzerdir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-151">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span>

![Sayfa denetçisinde ASP.NET MVC uygulaması](using-page-inspector-in-aspnet-mvc/_static/image10.png)

<span data-ttu-id="8bc07-153">Bu öğreticide, hızlı gezinmek ve uygulamada değişiklikler yapmak için **HTML** ve **Stiller** sekmelerini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="8bc07-153">In this tutorial, you will use the **HTML** and **Styles** tabs to navigate quickly and make changes to the application.</span></span>

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a><span data-ttu-id="8bc07-154">Enableinceleme modu</span><span class="sxs-lookup"><span data-stu-id="8bc07-154">EnableInspection Mode</span></span>

<span data-ttu-id="8bc07-155">Sayfa denetçisini Inceleme moduna almak için, **Denetle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-155">To put Page Inspector into Inspection Mode, click the **Inspect** button.</span></span> <span data-ttu-id="8bc07-156">Denetleme modunda, fare işaretçisini işlenmiş sayfanın herhangi bir bölümünde tuttuğunuzda, karşılık gelen kaynak biçimlendirmesi veya kodu vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="8bc07-156">In Inspection Mode, when you hold the mouse pointer over any part of the rendered page, the corresponding source markup or code is highlighted.</span></span>

![Inceleme modunu değiştirme](using-page-inspector-in-aspnet-mvc/_static/image12.png)

<span data-ttu-id="8bc07-158">Şimdi farenizi sayfa denetçisi içinde sayfanın farklı bölümlerine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-158">Now move your mouse over different parts of the page within Page Inspector.</span></span> <span data-ttu-id="8bc07-159">Yaptığınız gibi fare işaretçisi büyük artı işaretine dönüşür ve alttaki öğe vurgulanır:</span><span class="sxs-lookup"><span data-stu-id="8bc07-159">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Div üzerinde vurgulama. içerik-sarmalayıcı](using-page-inspector-in-aspnet-mvc/_static/image14.png)

<span data-ttu-id="8bc07-161">Fare işaretçisini taşırken, Visual Studio kaynak dosyada karşılık gelen Razor söz dizimi vurgular.</span><span class="sxs-lookup"><span data-stu-id="8bc07-161">As you move the mouse pointer, Visual Studio highlights the corresponding Razor syntax in the source file.</span></span> <span data-ttu-id="8bc07-162">HTML öğesi başka bir kaynak dosyasından geliyorsa, Visual Studio dosyayı otomatik olarak açar.</span><span class="sxs-lookup"><span data-stu-id="8bc07-162">If the HTML element comes from another source file, Visual Studio automatically opens the file.</span></span>

<span data-ttu-id="8bc07-163">Sayfa denetçisinde, **HTML** sekmesi Razor söz DIZIMI oluşturulan HTML 'yi gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-163">In Page Inspector, the **HTML** tab shows the HTML that was generated from the Razor syntax.</span></span> <span data-ttu-id="8bc07-164">Fare işaretçisini taşırken, HTML öğeleri vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="8bc07-164">As you move the mouse pointer, the HTML elements are highlighted.</span></span> <span data-ttu-id="8bc07-165">**Stiller** sekmesi Öğesı için CSS kurallarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-165">The **Styles** tab shows the CSS rules for the element.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="8bc07-166">Işaretlemede değişiklik yapmak için sayfa denetçisini kullanın</span><span class="sxs-lookup"><span data-stu-id="8bc07-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="8bc07-167">Sayfa denetçisi, konumu açık olmayabilir olan biçimlendirmeyi bulmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bc07-167">Page Inspector lets you find markup whose location might not be obvious.</span></span> <span data-ttu-id="8bc07-168">Ardından, biçimlendirmeyi değiştirebilir ve elde edilen değişiklikleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-168">Then you can modify the markup and see the resulting changes.</span></span>

<span data-ttu-id="8bc07-169">Bunu görmek için, **İncele** ' ye tıklayın ve ardından sayfa denetçisi penceresinde sayfanın en altına gidin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-169">To see this, click **Inspect** and then scroll to the bottom of the page in the Page Inspector window.</span></span>

<span data-ttu-id="8bc07-170">Fare işaretçisini altbilgi alanına taşıdığınızda, sayfa denetçisi \_Layout. cshtml dosyasını açar ve seçtiğiniz düzen sayfasının bölümünü vurgular.</span><span class="sxs-lookup"><span data-stu-id="8bc07-170">When you move the mouse pointer into the footer area, Page Inspector opens the \_Layout.cshtml file and highlights the section of the layout page that you have selected.</span></span> <span data-ttu-id="8bc07-171">Gördüğünüz gibi, alt bilgi, görünümün kendisi değil, düzen dosyasında tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8bc07-171">As you can see, the footer are is defined in the layout file, and not the view itself.</span></span>

![Arasında](using-page-inspector-in-aspnet-mvc/_static/image16.png)

<span data-ttu-id="8bc07-173">Artık fare işaretçinizi, telif hakkı <a id="a"> </a>bildiriminin bulunduğu çizginin üzerine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-173">Now move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span> <span data-ttu-id="8bc07-174">\_Layout. cshtml sayfasında, karşılık gelen çizgi vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="8bc07-174">In the \_Layout.cshtml page, the corresponding line is highlighted.</span></span>

![Alt bilgi için telif hakkı satırı vurgulanmış](using-page-inspector-in-aspnet-mvc/_static/image18.png)

<span data-ttu-id="8bc07-176">\_Layout. cshtml dosyasındaki satırın sonuna bir metin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-176">Add some text to the end of the line in the \_Layout.cshtml file.</span></span>

<span data-ttu-id="8bc07-177">&lt;p&gt;&amp;kopyalama; @DateTime.Now.Year-My ASP.NET MVC uygulaması Rolaları!&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="8bc07-177">&lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET MVC Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="8bc07-178">Şimdi, sayfa denetçisi tarayıcı penceresinde sonuçları görmek için CTRL + ALT + ENTER tuşlarına basın veya güncelleştirme çubuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-178">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![ASP.NET uygulamamın özellikleri!](using-page-inspector-in-aspnet-mvc/_static/image20.png)

<span data-ttu-id="8bc07-180">Alt bilginin Index. cshtml 'de tanımlandığını düşündük, ancak \_Layout. cshtml dosyasında olduğunu ve sayfa denetçisi sizin için bulmuştur.</span><span class="sxs-lookup"><span data-stu-id="8bc07-180">You might have thought that the footer defined in Index.cshtml, but it turned out to be in the \_Layout.cshtml, and Page Inspector found it for you.</span></span>

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="8bc07-181">İnceleme modu ve HTML penceresi</span><span class="sxs-lookup"><span data-stu-id="8bc07-181">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="8bc07-182">Daha sonra, HTML penceresine ve sizin için öğeleri nasıl eşlediği hakkında hızlı bir görünüme sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-182">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="8bc07-183">Inceleme moduna sayfa denetçisi koymak için **Denetle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-183">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="8bc07-184">Sayfanın "buraya logonuzu" belirten üst kısmına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-184">Click the top part of the page that says "Your logo here".</span></span> <span data-ttu-id="8bc07-185">Belirli bir öğeyi daha ayrıntılı bir şekilde inceleriz, bu nedenle fare işaretçisini taşırken tarayıcı penceresinde görüntüleme artık görünmez.</span><span class="sxs-lookup"><span data-stu-id="8bc07-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="8bc07-186">Şimdi, fare işaretçisini **HTML** penceresine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="8bc07-187">Fare işaretçisini taşırken, sayfa denetçisi **HTML** penceresi içindeki öğeyi özetler ve tarayıcı penceresinde buna karşılık gelen öğeyi vurgular.</span><span class="sxs-lookup"><span data-stu-id="8bc07-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML penceresi](using-page-inspector-in-aspnet-mvc/_static/image22.png)

<span data-ttu-id="8bc07-189">Daha önce olduğu gibi, sayfa denetçisi geçici bir sekmede sizin için \_Layout. cshtml dosyasını açar. \_Layout. cshtml geçici sekmesine tıklayın ve ilgili biçimlendirme, sizin için &lt;üst bilgi&gt; bölümünde vurgulanacaktır:</span><span class="sxs-lookup"><span data-stu-id="8bc07-189">As before, Page Inspector opens the \_Layout.cshtml file for you in a temporary tab. Click the \_Layout.cshtml temporary tab, and the corresponding markup will be highlighted in the &lt;header&gt; section for you:</span></span>

![Vurgulanan işaretleme](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="8bc07-191">Stiller penceresinde CSS değişikliklerinin önizlemesi</span><span class="sxs-lookup"><span data-stu-id="8bc07-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="8bc07-192">Daha sonra, CSS değişikliklerini önizlemek için sayfa denetçisi **stilleri** penceresini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="8bc07-192">Next, you will use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="8bc07-193">Inceleme moduna sayfa denetçisi koymak için **Denetle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-193">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="8bc07-194">Sayfa denetçisi tarayıcı penceresinde, **div. Content-Wrapper** etiketi görünene kadar fare Işaretçisini "giriş sayfası" bölümünün üzerine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![Div üzerinde vurgulama. içerik-sarmalayıcı](using-page-inspector-in-aspnet-mvc/_static/image26.png)

<span data-ttu-id="8bc07-196">Div. Content-Wrapper bölümünün içine bir kez tıklayın ve sonra fare işaretçisini **Stiller** penceresine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="8bc07-197">**Stiller** penceresi, bu öğe IÇIN tüm CSS kurallarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-197">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="8bc07-198">. Öne çıkan. Content-Wrapper sınıf seçiciyi bulmak için aşağı kaydırın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-198">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="8bc07-199">Şimdi arka plan rengi özelliği için onay kutusunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-199">Now clear the checkbox for the background-color property.</span></span>

![Arka plan rengini temizle](using-page-inspector-in-aspnet-mvc/_static/image28.png)

<span data-ttu-id="8bc07-201">Sayfa denetçisi tarayıcı penceresinde değişikliğin anında nasıl önizlediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-201">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="8bc07-202">Onay kutusunu yeniden seçin, sonra özellik değerine çift tıklayın ve kırmızı olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-202">Select the checkbox again, then double-click the property value and change it to red.</span></span> <span data-ttu-id="8bc07-203">Değişiklik hemen görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="8bc07-203">The change shows immediately:</span></span>

![Kırmızı arka plan rengi](using-page-inspector-in-aspnet-mvc/_static/image30.png)

<span data-ttu-id="8bc07-205">**Stiller** penceresi, değişiklikleri stil sayfasına IŞLEMEDEN önce CSS değişikliklerinin test edilmesi ve önizlenmesi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="8bc07-205">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="8bc07-206">CSS otomatik eşitleme</span><span class="sxs-lookup"><span data-stu-id="8bc07-206">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="8bc07-207">Bu özellik, sayfa denetçisinin 1,3 sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-207">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="8bc07-208">CSS otomatik eşitleme özelliği, bir CSS dosyasını doğrudan düzenlemenizi sağlar ve değişiklikleri sayfa denetçisi tarayıcısında hemen görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-208">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="8bc07-209">Inceleme moduna sayfa denetçisi koymak için **Denetle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-209">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="8bc07-210">Sayfa denetçisi tarayıcısında, **div. Content-Wrapper** etiketi görünene kadar fare Işaretçisini "giriş sayfası" bölümünün üzerine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-210">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="8bc07-211">Bu öğeyi seçmek için bir kez tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-211">Click once to select this element.</span></span>

<span data-ttu-id="8bc07-212">**Stiller** penceresi, bu öğe IÇIN tüm CSS kurallarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-212">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="8bc07-213">. Öne çıkan. Content-Wrapper sınıf seçiciyi bulmak için aşağı kaydırın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-213">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="8bc07-214">". Öne çıkan. içerik-sarmalayıcı" seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-214">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="8bc07-215">Sayfa denetçisi, bu stili (site. css) tanımlayan CSS dosyasını açar ve ilgili CSS stilini vurgular.</span><span class="sxs-lookup"><span data-stu-id="8bc07-215">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

<span data-ttu-id="8bc07-216">Şimdi `background-color` değerini "Red" olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-216">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="8bc07-217">Değişiklik, sayfa denetçisi tarayıcısında hemen görünür.</span><span class="sxs-lookup"><span data-stu-id="8bc07-217">The change appears immediately in the Page Inspector browser.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a><span data-ttu-id="8bc07-218">CSS renk seçiciyi kullanma</span><span class="sxs-lookup"><span data-stu-id="8bc07-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="8bc07-219">Visual Studio 2012 ' deki CSS Düzenleyicisi, renkleri seçip eklemeyi kolaylaştıran bir renk seçicisine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-219">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="8bc07-220">Renk Seçici standart bir renk paleti içerir, standart renk adlarını, karma kodları, RGB, RGBA, HSL ve HSLA renklerini destekler ve belgede en son kullandığınız renklerin bir listesini tutar.</span><span class="sxs-lookup"><span data-stu-id="8bc07-220">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="8bc07-221">Önceki bölümde `background-color` özelliğinin değerini değiştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-221">In the previous section, you changed the value of the `background-color` property.</span></span> <span data-ttu-id="8bc07-222">Renk seçiciyi çağırmak için, ekleme noktasını özellik adından sonra yerleştirin ve **#** ya da **RGB (** ) yazın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-222">To invoke the color picker, place the insertion point after the property name and type **#** or **rgb(**.</span></span>

![CSS Renk Seçici Çubuğu](using-page-inspector-in-aspnet-mvc/_static/image36.png)

<span data-ttu-id="8bc07-224">Seçmek için bir renge tıklayın veya aşağı ok tuşuna basın, sonra renkler arasında çapraz geçiş yapmak için sol ve sağ ok tuşlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-224">Click on a color to select it, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="8bc07-225">Bir rengi ziyaret ettiğinizde, karşılık gelen onaltılı değer önizlenebilir:</span><span class="sxs-lookup"><span data-stu-id="8bc07-225">When you visit a color, the corresponding hex value is previewed:</span></span>

![arka plan rengi Özellik değeri önizlenen](using-page-inspector-in-aspnet-mvc/_static/image38.png)

<span data-ttu-id="8bc07-227">Renk çubuğu tam istediğiniz renge sahip değilse, renk seçici açılır penceresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-227">If the color bar doesn't have the exact color you want, you can use the color picker pop-down.</span></span> <span data-ttu-id="8bc07-228">Açmak için, renk çubuğunun sağ ucundaki çift köşeli çift ayraca tıklayın veya klavyede bir kez veya iki kez aşağı ok tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-228">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS Renk Seçici açılır menüsü](using-page-inspector-in-aspnet-mvc/_static/image40.png)

<span data-ttu-id="8bc07-230">Sağ taraftaki dikey çubuktan bir renge tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-230">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="8bc07-231">Bu, ana penceredeki bu renk için bir gradyan gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-231">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="8bc07-232">ENTER tuşuna basarak doğrudan dikey çubuktan bir renk seçin veya ana penceredeki herhangi bir noktaya tıklayarak daha fazla duyarlık seçin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-232">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="8bc07-233">Bilgisayar ekranınızda kullanmak istediğiniz bir renk varsa (Visual Studio Kullanıcı arabirimi içinde olması gerekmez), sağ alt köşedeki Damlalık aracını kullanarak değerini yakalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-233">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="8bc07-234">Ayrıca renk seçicinin alt kısmına kaydırıcıyı taşıyarak bir rengin saydamlığını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-234">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="8bc07-235">Bunun yapılması, RGBA biçimi geçirgenliği temsil ettiğinden, renk değerlerini RGBA değerlerine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="8bc07-235">Doing so changes color values to RGBA values, because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="8bc07-236">Bir renk seçtikten sonra, ENTER tuşuna basın ve ardından *site. css* dosyasındaki arka plan rengi girişini tamamlamaya yönelik bir noktalı virgül yazın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-236">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="8bc07-237">Sayfa denetçisi güncelleştirme çubuğu</span><span class="sxs-lookup"><span data-stu-id="8bc07-237">The Page Inspector Update Bar</span></span>

<span data-ttu-id="8bc07-238">Sayfa denetçisi, *site. css* dosyasındaki değişikliği hemen algılar ve bir güncelleştirme çubuğunda bir uyarı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8bc07-238">Page Inspector immediately detects the change to the *Site.css* file and displays an alert in an update bar.</span></span>

![Güncelleştirme çubuğu](using-page-inspector-in-aspnet-mvc/_static/image42.png)

<span data-ttu-id="8bc07-240">Tüm dosyalarınızı kaydetmek ve sayfa denetçisi tarayıcısını yenilemek için CTRL + ALT + ENTER tuşlarına basın veya güncelleştirme çubuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-240">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="8bc07-241">Vurgu renginizdeki değişiklik tarayıcıda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-241">The change in the highlight color appears in the browser.</span></span>

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a><span data-ttu-id="8bc07-242">Dinamik sayfa öğelerini JavaScript 'e eşleme</span><span class="sxs-lookup"><span data-stu-id="8bc07-242">Mapping Dynamic Page Elements to JavaScript</span></span>

<span data-ttu-id="8bc07-243">Modern Web uygulamalarında, sayfadaki öğeler genellikle JavaScript ile dinamik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8bc07-243">In modern web applications, elements in the page are often generated dynamically with JavaScript.</span></span> <span data-ttu-id="8bc07-244">Bu, Bu sayfa öğelerine karşılık gelen statik biçimlendirme (HTML ya da Razor) olmadığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-244">That means there is no static markup (either HTML or Razor) that corresponds to these page elements.</span></span>

<span data-ttu-id="8bc07-245">Sürüm 1,3 ile, sayfa denetçisi artık sayfaya otomatik olarak eklenen öğeleri ilgili JavaScript koduna geri eşleyebilir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-245">With version 1.3, Page Inspector can now map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span> <span data-ttu-id="8bc07-246">Bu özelliği göstermek için [tek sayfalı uygulama (Spa) şablonunu](../../../single-page-application/overview/introduction/knockoutjs-template.md)kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="8bc07-246">To demonstrate this feature, we'll use the [Single Page Application (SPA) template](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8bc07-247">SPA şablonu [ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650) güncelleştirmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-247">The SPA template requires the [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) update.</span></span>

<span data-ttu-id="8bc07-248">Visual Studio 'da **dosya** &gt; **Yeni proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-248">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="8bc07-249">Sol tarafta, **C#görsel**' i genişletin, **Web**' i seçin ve **ASP.net MVC4 Web uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-249">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span> <span data-ttu-id="8bc07-250">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-250">Click **OK**.</span></span>

<span data-ttu-id="8bc07-251">**Yeni ASP.NET MVC 4 proje** Iletişim kutusunda **tek sayfalı uygulama**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-251">In the **New ASP.NET MVC 4 Project** dialog, select **Single Page Application**.</span></span>

<span data-ttu-id="8bc07-252">Çözüm Gezgini ' de, **Görünümler** klasörünü ve ardından **giriş** klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-252">In Solution Explorer, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="8bc07-253">Index. cshtml dosyasına sağ tıklayın ve **sayfa denetçisinde görüntüle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-253">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

<span data-ttu-id="8bc07-254">Sayfa denetçisi tarayıcısında görüntülenen ilk şey bir oturum açma sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="8bc07-254">The first thing that is displayed in the Page Inspector browser is a login page.</span></span> <span data-ttu-id="8bc07-255">"Kaydolun" a tıklayın ve bir Kullanıcı adı ve parola oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8bc07-255">Click "Sign Up" and create a user name and password.</span></span> <span data-ttu-id="8bc07-256">Kaydolduktan sonra uygulama oturumunuzu açar ve bazı örnek öğelerle bir yapılacaklar listesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8bc07-256">Once you sign up, the application logs you in and creates a to-do list with some sample items.</span></span>

<span data-ttu-id="8bc07-257">Inceleme moduna sayfa denetçisi koymak için **Denetle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-257">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span> <span data-ttu-id="8bc07-258">Sayfa denetçisi tarayıcısında, yapılacaklar öğelerinden birine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bc07-258">In the Page Inspector browser, click on one of the to-do items.</span></span> <span data-ttu-id="8bc07-259">Mavi renkle vurgulanacak, öğe adının yanında "JS" ile Turuncu renkle vurgulandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8bc07-259">Notice that instead of being highlighted in blue, the element is highlighted in orange, with "JS" next to the element name.</span></span> <span data-ttu-id="8bc07-260">Bu, öğesinin betik aracılığıyla dinamik olarak oluşturulduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-260">This indicates that the element was created dynamically through script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

<span data-ttu-id="8bc07-261">Ayrıca, **çağrı yığını** sekmesinde turuncu bir alt çizgi görünür. Bu, **çağrı yığını** bölmesinin öğesi hakkında daha fazla bilgi olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-261">In addition, an orange underline appears on the **Call Stack** tab. This indicates that the **Call Stack** pane has more information about the element.</span></span>

<span data-ttu-id="8bc07-262">**Çağrı yığını** sekmesine tıklayın. **Çağrı yığını** bölmesi, öğesini oluşturan JavaScript çağrısının çağrı yığınını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bc07-262">Click on the **Call Stack** tab. The **Call Stack** pane shows the call stack for the JavaScript call that created the element.</span></span> <span data-ttu-id="8bc07-263">JQuery gibi dış kitaplıklara yapılan çağrılar daraltılır, böylece uygulama betiğe yönelik çağrıları kolayca görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-263">Calls to external libraries such as jQuery are collapsed, so that you can easily see the calls to your application script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

<span data-ttu-id="8bc07-264">Dış kitaplıklara yapılan çağrılar dahil olmak üzere tam yığını görmek için, "dış kitaplıklar" etiketli düğümleri genişletebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8bc07-264">To see the full stack, including calls to external libraries, you can expand the nodes labeled "External Libraries":</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

<span data-ttu-id="8bc07-265">Çağrı yığınında bir öğeye tıklarsanız, Visual Studio kod dosyasını açar ve ilgili betiği vurgular.</span><span class="sxs-lookup"><span data-stu-id="8bc07-265">If you click an item in the call stack, Visual Studio opens the code file and highlights the corresponding script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a><span data-ttu-id="8bc07-266">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8bc07-266">See Also</span></span>

<span data-ttu-id="8bc07-267">[Visual Studio ile ASP.NET MVC 4 ' e giriş](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.NET Web sitesi)</span><span class="sxs-lookup"><span data-stu-id="8bc07-267">[Intro to ASP.NET MVC 4 with Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net website)</span></span>

<span data-ttu-id="8bc07-268">[Sayfa denetçisi Ile tanışın](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 Videosu)</span><span class="sxs-lookup"><span data-stu-id="8bc07-268">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 video)</span></span>

<span data-ttu-id="8bc07-269">[Sayfa denetçisi hata iletileri](https://go.microsoft.com/?linkid=9813062) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="8bc07-269">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
