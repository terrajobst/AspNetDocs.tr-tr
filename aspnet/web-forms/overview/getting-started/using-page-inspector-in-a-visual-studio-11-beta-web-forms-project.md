---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: ASP.NET Web Forms Visual Studio 2012 için sayfa denetçisi 'ni kullanma | Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 için sayfa denetçisi, tümleşik bir tarayıcıyla bir Web geliştirme aracıdır. Tümleşik tarayıcıda ve sayfa denetçisinde herhangi bir öğe seçin...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: c165bbea505b4cb8eae1312cdd587f4ed36541a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575924"
---
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a><span data-ttu-id="6b820-104">ASP.NET Web Forms’da Visual Studio 2012 için Sayfa Denetçisini Kullanma</span><span class="sxs-lookup"><span data-stu-id="6b820-104">Using Page Inspector for Visual Studio 2012 in ASP.NET Web Forms</span></span>

<span data-ttu-id="6b820-105">, Tim Ammann tarafından</span><span class="sxs-lookup"><span data-stu-id="6b820-105">by Tim Ammann</span></span>

> <span data-ttu-id="6b820-106">Visual Studio 2012 için sayfa denetçisi, tümleşik bir tarayıcıyla bir Web geliştirme aracıdır.</span><span class="sxs-lookup"><span data-stu-id="6b820-106">Page Inspector for Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="6b820-107">Tümleşik tarayıcıda herhangi bir öğeyi seçin ve sayfa denetçisi öğenin kaynağını ve CSS 'sini anında vurgular.</span><span class="sxs-lookup"><span data-stu-id="6b820-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="6b820-108">Uygulamanızdaki herhangi bir sayfaya gözatabilir, işlenmiş biçimlendirmenin kaynaklarını hızlıca bulabilir ve Visual Studio ortamında doğrudan tarayıcı araçları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b820-108">You can browse any page in your application, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> <span data-ttu-id="6b820-109">Bu öğreticide Inceleme modunun nasıl etkinleştirileceği ve ardından Web projenizdeki CSS kuralları ile metinlerin hızlı bir şekilde nasıl konumlandırmaları ve düzenlenmesi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6b820-109">This tutorial shows how to enable Inspection Mode and then quickly locate and edit CSS rules and text within your web project.</span></span> <span data-ttu-id="6b820-110">Öğretici bir Web Forms uygulama projesi kullanır, ancak Web sitesi projeleri ve [MVC](https://go.microsoft.com/?linkid=9802002) uygulamaları Için sayfa denetçisi 'ni de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b820-110">The tutorial uses a Web Forms Application Project, but you can also use Page Inspector for Web Site projects and [MVC](https://go.microsoft.com/?linkid=9802002) applications.</span></span>
> 
> <span data-ttu-id="6b820-111">Öğreticide aşağıdaki bölümler bulunur:</span><span class="sxs-lookup"><span data-stu-id="6b820-111">The tutorial has the following sections:</span></span>
> 
> [<span data-ttu-id="6b820-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6b820-112">Prerequisites</span></span>](#_1_prerequisites)
> 
> [<span data-ttu-id="6b820-113">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b820-113">Create a Web Application</span></span>](#_2_creating_a)
> 
> [<span data-ttu-id="6b820-114">Uygulamayı görüntülemek için sayfa denetçisini kullanma</span><span class="sxs-lookup"><span data-stu-id="6b820-114">Use Page Inspector to View the Application</span></span>](#_3_using_page)
> 
> [<span data-ttu-id="6b820-115">Inceleme modunu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6b820-115">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> 
> [<span data-ttu-id="6b820-116">Işaretlemede değişiklik yapmak için sayfa denetçisini kullanın</span><span class="sxs-lookup"><span data-stu-id="6b820-116">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> 
> [<span data-ttu-id="6b820-117">İnceleme modu ve HTML penceresi</span><span class="sxs-lookup"><span data-stu-id="6b820-117">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> 
> [<span data-ttu-id="6b820-118">Stiller penceresinde CSS değişikliklerinin önizlemesi</span><span class="sxs-lookup"><span data-stu-id="6b820-118">Preview CSS Changes in the Styles Window</span></span>](#_7_previewing_css)
> 
> [<span data-ttu-id="6b820-119">CSS otomatik eşitleme</span><span class="sxs-lookup"><span data-stu-id="6b820-119">CSS Auto Sync</span></span>](#css_auto_sync)
> 
> [<span data-ttu-id="6b820-120">CSS renk seçiciyi kullanma</span><span class="sxs-lookup"><span data-stu-id="6b820-120">Using the CSS Color Picker</span></span>](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="6b820-121">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6b820-121">Prerequisites</span></span>

- <span data-ttu-id="6b820-122">Web için [Visual Studio 2012](https://www.microsoft.com/visualstudio/11) veya [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span><span class="sxs-lookup"><span data-stu-id="6b820-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="6b820-123">Sayfa denetçisinin en son sürümünü almak için, .NET 2,0 için Azure SDK 'yı yüklemek üzere [Web Platformu Yükleyicisi](https://go.microsoft.com/fwlink/?LinkId=255386) 'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="6b820-123">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="6b820-124">Sayfa denetçisi Microsoft Web Geliştirici Araçları ile paketlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="6b820-124">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="6b820-125">En son sürüm 1,3 ' dir.</span><span class="sxs-lookup"><span data-stu-id="6b820-125">The latest version is 1.3.</span></span> <span data-ttu-id="6b820-126">Sahip olduğunuz sürümü denetlemek için, Visual Studio 'Yu çalıştırın ve **Yardım** menüsünden **Microsoft Visual Studio hakkında** ' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="6b820-126">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="6b820-127">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b820-127">Create a Web Application</span></span>

<span data-ttu-id="6b820-128">İlk olarak, ile sayfa denetçisi kullanacağınız bir Web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="6b820-128">First, you will create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="6b820-129">Visual Studio 'da **dosya** &gt; **Yeni proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="6b820-129">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="6b820-130">Sol tarafta, **görsel C#** ' i genişletin, **Web**' i seçin ve ardından **ASP.NET Web Forms uygulama**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="6b820-130">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET Web Forms Application**.</span></span>

![Yeni Web Forms uygulaması](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

<span data-ttu-id="6b820-132">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-132">Click **OK**.</span></span>

<span data-ttu-id="6b820-133">Uygulama **kaynak** görünümü ' nde açılır.</span><span class="sxs-lookup"><span data-stu-id="6b820-133">The application opens in **Source** view.</span></span>

![Kaynak görünümünde yeni Web Forms uygulaması](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

<span data-ttu-id="6b820-135">Artık birlikte çalışmak üzere bir uygulamanız olduğuna göre, sayfayı incelemek ve değiştirmek için sayfa denetçisi ' ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b820-135">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a><span data-ttu-id="6b820-136">Uygulamayı görüntülemek için sayfa denetçisini kullanma</span><span class="sxs-lookup"><span data-stu-id="6b820-136">Use Page Inspector to View the Application</span></span>

<span data-ttu-id="6b820-137">Daha sonra, uygulamayı sayfa denetçisi ile birlikte görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6b820-137">Next, you will view the application with Page Inspector.</span></span> <span data-ttu-id="6b820-138">**Çözüm Gezgini**' de projeye sağ tıklayın ve ardından **sayfa denetçisinde görüntüle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="6b820-138">In **Solution Explorer**, right click the project, and then choose **View in Page Inspector**.</span></span>

![Sayfa denetçisinde görüntüle](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

<span data-ttu-id="6b820-140">Varsayılan olarak, sayfa denetçisi ilk kez başlatıldığında, Visual Studio ortamının sol tarafında dar bir pencere olarak yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="6b820-140">By default, when Page Inspector launches for the first time, it is docked as a narrow window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="6b820-141">Sol tarafta bırakın ve bunu sizin için rahat olan bir genişliğe ayarlayın veya en üstteki, alttaki veya sağdaki araç alanlarından birine yerleştirin:</span><span class="sxs-lookup"><span data-stu-id="6b820-141">Leave it docked on the left side and set it to a width that is comfortable for you, or dock it in one of the tool areas on the top, bottom, or right:</span></span>

![Sayfa denetçisi yerleştirme konumları](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

<span data-ttu-id="6b820-143">Sayfa denetçisi penceresini çıkardıysanız, Visual Studio 'Nun dışına veya varsa ikinci bir monitöre yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b820-143">If you undock the Page Inspector window, you can place it outside Visual Studio, or even on a second monitor if you have one.</span></span> <span data-ttu-id="6b820-144">Bununla birlikte, sayfa denetçisi penceresi yok edildiğinde, sayfa denetçisi ve Visual Studio arasında ALT + TAB 'a giderek, **araçlar** &gt; **seçenekler** &gt; **ortam** &gt; **Sekmeler ve pencereler**' e gidin ve **sekme kutusu**' nun altında, **kayan araç pencereleri ' nin her zaman ana pencerenin en üstünde yer alan**onay kutusunun işaretini kaldırın:</span><span class="sxs-lookup"><span data-stu-id="6b820-144">However, in order to ALT+TAB between Page Inspector and Visual Studio when the Page Inspector window is undocked, go to **Tools** &gt; **Options** &gt; **Environment** &gt; **Tabs and Windows**, and under **Tab Well**, clear the check box called **Floating tool windows always stay on top of the main window**:</span></span>

![Kayan araç Windows onay kutusunu Visual Studio ve yerleştirilmemiş sayfa denetçisi penceresi arasında ALT + TAB olarak temizleyin](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

<span data-ttu-id="6b820-146">Sayfa denetçisi penceresinin üst bölmesi, geçerli sayfayı bir tarayıcı penceresinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b820-146">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="6b820-147">Alt bölmede, sol taraftaki HTML biçimlendirme sayfası ve sayfanın farklı yönlerini incelemenize olanak tanıyan bazı sekmeler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="6b820-147">The bottom pane shows the page in HTML markup on the left, and some tabs on the right that let you inspect different aspects of the page.</span></span> <span data-ttu-id="6b820-148">Alt bölme, Internet Explorer 'daki [F12 geliştirici araçları](https://msdn.microsoft.com/ie/aa740478) benzerdir.</span><span class="sxs-lookup"><span data-stu-id="6b820-148">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span> <span data-ttu-id="6b820-149">(Ancak, Geliştirici araçlarının aksine, Visual Studio 'da doğrudan sayfa denetçisi kullanabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="6b820-149">(However, unlike the developer tools, you can use Page Inspector right within Visual Studio.)</span></span>

![Sayfa Denetçisi](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

<span data-ttu-id="6b820-151">Bu öğreticide, hızlı bir şekilde gezinmenize ve uygulamada değişiklik yapmanıza yardımcı olması için sayfa denetçisi tarayıcı bölmesini ve **HTML** ve **Stiller** sekmelerini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="6b820-151">In this tutorial, you will use the Page Inspector browser pane, and the **HTML** and **Styles** tabs to help you rapidly navigate and make changes to the application.</span></span>

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a><span data-ttu-id="6b820-152">Inceleme modunu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6b820-152">Enable Inspection Mode</span></span>

<span data-ttu-id="6b820-153">Daha sonra, sayfa denetçisi Inceleme modunun nasıl çalıştığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6b820-153">Next, you will see how Page Inspector's Inspection Mode works.</span></span> <span data-ttu-id="6b820-154">Sayfa denetçisi penceresinde, **Denetle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-154">In the Page Inspector window, click the **Inspect** button.</span></span>

![Öğeyi İncele](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

<span data-ttu-id="6b820-156">İnceleme modunu çalışırken görmek için farenizi sayfa denetçisi tarayıcı penceresi içinde sayfanın farklı bölümlerine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="6b820-156">To see inspection mode in action, move your mouse over different parts of the page within the Page Inspector browser window.</span></span> <span data-ttu-id="6b820-157">Yaptığınız gibi fare işaretçisi büyük artı işaretine dönüşür ve alttaki öğe vurgulanır:</span><span class="sxs-lookup"><span data-stu-id="6b820-157">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Div üzerinde vurgulama. içerik-sarmalayıcı](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

<span data-ttu-id="6b820-159">Fare işaretçisini taşırken,</span><span class="sxs-lookup"><span data-stu-id="6b820-159">As you move the mouse pointer, note that</span></span>

- <span data-ttu-id="6b820-160">**Kaynak** görünümündeki içerikler, sayfadaki seçili öğeye karşılık gelen biçimlendirmeyi göstermek için değişir.</span><span class="sxs-lookup"><span data-stu-id="6b820-160">The content in **Source** view changes to show the markup corresponding to the selected element on the page.</span></span> <span data-ttu-id="6b820-161">İlgili biçimlendirme vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="6b820-161">The relevant markup is highlighted.</span></span> <span data-ttu-id="6b820-162">Kaynak başka bir dosya ise, bu dosya kaynak görünümünde ilgili biçimlendirme vurgulanarak açılır.</span><span class="sxs-lookup"><span data-stu-id="6b820-162">If the source is in another file, that file is opened in Source view with the relevant markup highlighted.</span></span>

- <span data-ttu-id="6b820-163">Sayfa denetçisindeki **HTML** sekmesinde görünen biçimlendirme Ayrıca sayfadaki seçili öğeye karşılık gelen şekilde değişir.</span><span class="sxs-lookup"><span data-stu-id="6b820-163">The markup displayed in the **HTML** tab in Page Inspector also changes to correspond to the selected element on the page.</span></span> <span data-ttu-id="6b820-164">**HTML** sekmesinde, ilgili biçimlendirme özetlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="6b820-164">In the **HTML** tab, the relevant markup is outlined.</span></span>

- <span data-ttu-id="6b820-165">**Stiller** sekmesi, geçerli SEÇIMLE ilgili CSS kurallarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b820-165">The **Styles** tab shows the CSS rules relevant to the current selection.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="6b820-166">Işaretlemede değişiklik yapmak için sayfa denetçisini kullanın</span><span class="sxs-lookup"><span data-stu-id="6b820-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="6b820-167">Şimdi, konumu bulma ve biçimlendirme veya metin üzerinde değişiklik yapmak için sayfa denetçisini nasıl kullanabileceğinizi göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6b820-167">Now you will see how you can use Page Inspector to find and make changes to markup or text whose location might not be immediately obvious.</span></span>

<span data-ttu-id="6b820-168">Sayfa denetçisi ' ni Inceleme moduna alın ve ardından giriş sayfasının en altına kaydırın.</span><span class="sxs-lookup"><span data-stu-id="6b820-168">Put Page Inspector in Inspection Mode and then scroll to the bottom of the home page.</span></span>

<span data-ttu-id="6b820-169">Alt bilgi alanını girdikten hemen sonra, sayfa denetçisi *site. Master* düzen dosyasını diğer sekmelerin sağındaki geçici bir sekmede açar ve seçtiğiniz ana sayfanın bölümünü vurgular.</span><span class="sxs-lookup"><span data-stu-id="6b820-169">As soon as you enter the footer area, Page Inspector opens the *Site.Master* layout file in **Source** view in a temporary tab to the right of the other tabs and highlights the section of the master page that you have selected.</span></span> <span data-ttu-id="6b820-170">Bu, sayfa denetçisinin, gerçekten açtığınız farklı bir dosyadan gelmiş olabilecek bir sayfada içerik bulma ve görüntüleme şeklini gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b820-170">This shows you how Page Inspector can find and display content on a page that might actually come from a different file than the one you originally opened.</span></span>

![Inceleme modundaki alt bilgi vurguları](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

<span data-ttu-id="6b820-172">Sayfa denetçisi tarayıcı penceresinde, fare işaretçinizi, telif hakkı <a id="a"> </a>bildiriminin bulunduğu çizginin üzerine getirin.</span><span class="sxs-lookup"><span data-stu-id="6b820-172">In the Page Inspector browser window, move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span>

<span data-ttu-id="6b820-173">*Site. Master* sayfasında, karşılık gelen çizgi vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="6b820-173">In the *Site.Master* page, the corresponding line is highlighted.</span></span>

![Alt bilgi için telif hakkı satırı vurgulanmış](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

<span data-ttu-id="6b820-175">*Site. Master* dosyasındaki satırın sonuna bir metin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6b820-175">Add some text to the end of the line in the *Site.Master* file.</span></span>

<span data-ttu-id="6b820-176">&lt;p&gt;&amp;kopyalama; &lt;%: DateTime. Now. Year%&gt;-My ASP.NET Application rol!&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="6b820-176">&lt;p&gt;&amp;copy; &lt;%: DateTime.Now.Year %&gt; - My ASP.NET Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="6b820-177">Şimdi, sayfa denetçisi tarayıcı penceresinde sonuçları görmek için CTRL + ALT + ENTER tuşlarına basın veya güncelleştirme çubuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-177">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![ASP.NET uygulamamın özellikleri!](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

<span data-ttu-id="6b820-179">Altbilginin *default. aspx* sayfasında olduğunu, ancak ana düzen sayfasında olduğunu düşündük ve sayfa denetçisi sizin için buldu.</span><span class="sxs-lookup"><span data-stu-id="6b820-179">You might have thought that the footer was on the *Default.aspx* page, but it turned out to be in the master layout page, and Page Inspector found it for you.</span></span>

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="6b820-180">İnceleme modu ve HTML penceresi</span><span class="sxs-lookup"><span data-stu-id="6b820-180">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="6b820-181">Daha sonra, HTML penceresine ve sizin için öğeleri nasıl eşlediği hakkında hızlı bir görünüme sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="6b820-181">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="6b820-182">Sayfa denetçisini Inceleme moduna alın.</span><span class="sxs-lookup"><span data-stu-id="6b820-182">Put Page Inspector in Inspection Mode.</span></span>

![Öğeyi İncele](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

<span data-ttu-id="6b820-184">Sayfanın "buraya logonuzu" belirten üst kısmına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-184">Click the top part of the page that says "your logo here".</span></span> <span data-ttu-id="6b820-185">Belirli bir öğeyi daha ayrıntılı bir şekilde inceleriz, bu nedenle fare işaretçisini taşırken tarayıcı penceresinde görüntüleme artık görünmez.</span><span class="sxs-lookup"><span data-stu-id="6b820-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="6b820-186">Şimdi, fare işaretçisini **HTML** penceresine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="6b820-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="6b820-187">Fare işaretçisini taşırken, sayfa denetçisi **HTML** penceresi içindeki öğeyi özetler ve tarayıcı penceresinde buna karşılık gelen öğeyi vurgular.</span><span class="sxs-lookup"><span data-stu-id="6b820-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML penceresi](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

<span data-ttu-id="6b820-189">Daha önce olduğu gibi, sayfa denetçisi *site. Master* dosyasını sizin için geçici bir sekmede açar. site. Master sekmesine tıklayın ve ilgili biçimlendirme &lt;üst bilgi&gt; bölümünde vurgulanır:</span><span class="sxs-lookup"><span data-stu-id="6b820-189">As before, Page Inspector opens the *Site.Master* file for you in a temporary tab. Click the Site.Master tab, and the corresponding markup is highlighted in the &lt;header&gt; section:</span></span>

![Vurgulanan işaretleme](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="6b820-191">Stiller penceresinde CSS değişikliklerinin önizlemesi</span><span class="sxs-lookup"><span data-stu-id="6b820-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="6b820-192">Daha sonra, CSS değişikliklerini önizlemek için sayfa denetçisi **stilleri** penceresini nasıl kullanabileceğinizi göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6b820-192">Next, you will see how you can use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="6b820-193">Inceleme moduna sayfa denetçisi koymak için **Denetle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-193">Click the **Inspect** button to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="6b820-194">Sayfa denetçisi tarayıcı penceresinde, **div. Content-Wrapper** etiketi görünene kadar fare Işaretçisini "giriş sayfası" bölümünün üzerine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="6b820-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![Öğelerin üzerine gelindiğinde](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

<span data-ttu-id="6b820-196">Div. Content-Wrapper bölümünün içine bir kez tıklayın ve sonra fare işaretçisini **Stiller** penceresine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="6b820-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="6b820-197">. Öne çıkan. Content-sarmalayıcı sınıfı seçicisinin altında, arka plan rengi özelliği için onay kutusunu temizleyin ve seçin.</span><span class="sxs-lookup"><span data-stu-id="6b820-197">Under the .featured .content-wrapper class selector, clear and select the checkbox for the background-color property.</span></span>

![Arka plan rengini temizle](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

<span data-ttu-id="6b820-199">Sayfa denetçisi tarayıcı penceresinde değişikliğin anında nasıl önizlediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6b820-199">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="6b820-200">Onay kutusunu yeniden seçin, sonra özellik değerini çift tıklatın ve `red`değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6b820-200">Select the checkbox again, then double-click the property value and change it to `red`.</span></span> <span data-ttu-id="6b820-201">Değişiklik hemen görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="6b820-201">The change shows immediately:</span></span>

![Kırmızı arka plan rengi](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

<span data-ttu-id="6b820-203">**Stiller** penceresi, değişiklikleri stil sayfasına IŞLEMEDEN önce CSS değişikliklerinin test edilmesi ve önizlenmesi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="6b820-203">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="6b820-204">CSS otomatik eşitleme</span><span class="sxs-lookup"><span data-stu-id="6b820-204">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="6b820-205">Bu özellik, sayfa denetçisinin 1,3 sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6b820-205">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="6b820-206">CSS otomatik eşitleme özelliği, bir CSS dosyasını doğrudan düzenlemenizi sağlar ve değişiklikleri sayfa denetçisi tarayıcısında hemen görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b820-206">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="6b820-207">Inceleme moduna sayfa denetçisi koymak için **Denetle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-207">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="6b820-208">Sayfa denetçisi tarayıcısında, **div. Content-Wrapper** etiketi görünene kadar fare Işaretçisini "giriş sayfası" bölümünün üzerine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="6b820-208">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="6b820-209">Bu öğeyi seçmek için bir kez tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-209">Click once to select this element.</span></span>

<span data-ttu-id="6b820-210">**Stiller** penceresi, bu öğe IÇIN tüm CSS kurallarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b820-210">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="6b820-211">. Öne çıkan. Content-Wrapper sınıf seçiciyi bulmak için aşağı kaydırın.</span><span class="sxs-lookup"><span data-stu-id="6b820-211">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="6b820-212">". Öne çıkan. içerik-sarmalayıcı" seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-212">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="6b820-213">Sayfa denetçisi, bu stili (site. css) tanımlayan CSS dosyasını açar ve ilgili CSS stilini vurgular.</span><span class="sxs-lookup"><span data-stu-id="6b820-213">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![CSS dosyası](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

<span data-ttu-id="6b820-215">Şimdi `background-color` değerini "Red" olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6b820-215">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="6b820-216">Değişiklik, sayfa denetçisi tarayıcısında hemen görünür.</span><span class="sxs-lookup"><span data-stu-id="6b820-216">The change appears immediately in the Page Inspector browser.</span></span>

![Sayfa denetçisi tarayıcısı](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a><span data-ttu-id="6b820-218">CSS renk seçiciyi kullanma</span><span class="sxs-lookup"><span data-stu-id="6b820-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="6b820-219">Daha sonra, varsayılan uygulamada Vurgulanan metin için CSS 'yi hızlı bir şekilde bulmak ve değiştirmek üzere sayfa denetçisi 'ni nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6b820-219">Next, you'll learn how to use Page Inspector to quickly find and change the CSS for highlighted text in the default application.</span></span> <span data-ttu-id="6b820-220">Bu örnekte, mavi vurgulamayı beğenmemenizi ve bunu başka bir renkle değiştirmek istediğinizi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="6b820-220">In this example, you've decided that you don't like the blue highlighting and want to change it to another color.</span></span>

<span data-ttu-id="6b820-221">**Denetle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-221">Click the **Inspect** button.</span></span>

![Öğeyi İncele](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

<span data-ttu-id="6b820-223">Sayfa denetçisi tarayıcı penceresinde, CSS "Mark" etiketinin görünmesi için fare işaretçisini vurgulanan "videolar, öğreticiler ve örnekler" metninin üzerine taşıyın.</span><span class="sxs-lookup"><span data-stu-id="6b820-223">In the Page Inspector browser window, move the mouse pointer over the highlighted "videos, tutorials, and samples" text so that the CSS "mark" label appears.</span></span>

![Mark öğesinin üzerine gelindiğinde](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

<span data-ttu-id="6b820-225">Seçmek için metne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-225">Click the text to select it.</span></span> <span data-ttu-id="6b820-226">Karşılık gelen CSS işaret Seçicisi, **Stiller** penceresinin alt kısmında görünür.</span><span class="sxs-lookup"><span data-stu-id="6b820-226">The corresponding CSS mark selector appears at the bottom of the **Styles** window.</span></span>

![Stiller penceresinde işaret Seçicisi](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

<span data-ttu-id="6b820-228">İşaret seçicisine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-228">Click the mark selector.</span></span> <span data-ttu-id="6b820-229">Bu, Web uygulaması için *site. css* dosyasını açar.</span><span class="sxs-lookup"><span data-stu-id="6b820-229">This opens the *Site.css* file for the web application.</span></span> <span data-ttu-id="6b820-230">Site. css sekmesine tıklayın ve seçici için karşılık gelen CSS vurgulanır:</span><span class="sxs-lookup"><span data-stu-id="6b820-230">Click the Site.css tab, and the corresponding CSS for the selector is highlighted:</span></span>

![stil sayfasında işaret Seçicisi](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

<span data-ttu-id="6b820-232">Arka plan rengi özelliği ile satırı seçin ve kaldırın.</span><span class="sxs-lookup"><span data-stu-id="6b820-232">Select and remove the line with the background-color property.</span></span>

<span data-ttu-id="6b820-233">Şimdi **işaretle** arkaplan-Color özelliği için yeni bir renk seçmek üzere yeni Visual STUDIO 2012 CSS renk seçiciyi kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="6b820-233">You will now use the new Visual Studio 2012 CSS color picker to choose a new color for the **mark** background-color property.</span></span>

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a><span data-ttu-id="6b820-234">Visual Studio 2012 CSS renk seçiciyi kullanma</span><span class="sxs-lookup"><span data-stu-id="6b820-234">Using the Visual Studio 2012 CSS Color Picker</span></span>

<span data-ttu-id="6b820-235">Visual Studio 2012 ' deki CSS Düzenleyicisi, renkleri seçip eklemeyi kolaylaştıran bir renk seçicisine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6b820-235">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="6b820-236">Basit bir renk çubuğuna ve daha hassas denetim sağlayan bir "açılır" seçicisine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6b820-236">It has a simple color bar and a "pop-down" picker that offers finer control.</span></span>

<span data-ttu-id="6b820-237">Renk Seçici standart bir renk paleti içerir, standart renk adlarını, karma kodları, RGB, RGBA, HSL ve HSLA renklerini destekler ve belgede en son kullandığınız renklerin bir listesini tutar.</span><span class="sxs-lookup"><span data-stu-id="6b820-237">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="6b820-238">Arka plan rengi özelliğinin olduğu satırda "BC" yazın ve aşağı oka bir kez basın.</span><span class="sxs-lookup"><span data-stu-id="6b820-238">On the line where the background-color property was, type "bc" and press the down arrow once.</span></span>

<span data-ttu-id="6b820-239">Her sözcüğün ilk karakterini "Arkaplan-Color" gibi bir tire ayrılmış özellikte yazdığınızda, IntelliSense yalnızca eşleşen özellikleri göstermek için listeyi filtreler:</span><span class="sxs-lookup"><span data-stu-id="6b820-239">When you type the first character of each word in a hyphen-separated property like "background-color", IntelliSense filters the list for you to show only the properties that match:</span></span>

![IntelliSense filtrelenmiş değerler](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

<span data-ttu-id="6b820-241">Şimdi bir iki nokta üst üste yazın.</span><span class="sxs-lookup"><span data-stu-id="6b820-241">Now type a colon.</span></span> <span data-ttu-id="6b820-242">Bunu yaptığınızda, tam arka plan rengi Özellik adı eklenir.</span><span class="sxs-lookup"><span data-stu-id="6b820-242">When you do, the full background-color property name is inserted.</span></span> <span data-ttu-id="6b820-243">**#** veya **RGB yazın (** ve renk seçici çubuğu görünür:</span><span class="sxs-lookup"><span data-stu-id="6b820-243">Type **#** or **rgb(**, and the color picker bar appears:</span></span>

![CSS Renk Seçici Çubuğu](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

<span data-ttu-id="6b820-245">Renk seçici çubuğunun nasıl çalıştığını görmek için fare işaretçisi ile renklerini tıklatın veya aşağı ok tuşuna basın ve ardından sağ ve sağ ok tuşlarını kullanarak renkleri çapraz geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="6b820-245">To see how the color picker bar works, click its colors with the mouse pointer, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="6b820-246">Bir rengi ziyaret ettiğinizde, arka plan rengi özelliği için karşılık gelen değer önizlenebilir:</span><span class="sxs-lookup"><span data-stu-id="6b820-246">When you visit a color, the corresponding value for the background-color property is previewed:</span></span>

![arka plan rengi Özellik değeri önizlenen](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

<span data-ttu-id="6b820-248">Bu noktada, değeri seçmek için ENTER tuşuna basabilir ve sonra noktalı virgül (;) CSS girdisini doldurun.</span><span class="sxs-lookup"><span data-stu-id="6b820-248">At this point, you could press Enter to select the value and then a semicolon (;) to complete the CSS entry.</span></span> <span data-ttu-id="6b820-249">Şimdilik renk seçici açılır ekranının nasıl çalıştığını görebilmeniz için sonraki bölüme gidin.</span><span class="sxs-lookup"><span data-stu-id="6b820-249">For now, go on to the next section so that you can see how the color picker pop-down works.</span></span>

#### <a name="using-the-color-picker-pop-down"></a><span data-ttu-id="6b820-250">Renk Seçici açılır penceresini kullanma</span><span class="sxs-lookup"><span data-stu-id="6b820-250">Using the Color Picker Pop-Down</span></span>

<span data-ttu-id="6b820-251">Renk çubuğu Aradığınız renge sahip olmadığında renk seçici açılır penceresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b820-251">When the color bar doesn't have the exact color that you're looking for, you can use the color picker pop-down.</span></span>

<span data-ttu-id="6b820-252">Açmak için, renk çubuğunun sağ ucundaki çift köşeli çift ayraca tıklayın veya klavyede bir kez veya iki kez aşağı ok tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="6b820-252">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS Renk Seçici açılır menüsü](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

<span data-ttu-id="6b820-254">Sağ taraftaki dikey çubuktan bir renge tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-254">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="6b820-255">Bu, ana penceredeki bu renk için bir gradyan gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b820-255">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="6b820-256">ENTER tuşuna basarak doğrudan dikey çubuktan bir renk seçin veya ana penceredeki herhangi bir noktaya tıklayarak daha fazla duyarlık seçin.</span><span class="sxs-lookup"><span data-stu-id="6b820-256">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="6b820-257">Bilgisayar ekranınızda kullanmak istediğiniz bir renk varsa (Visual Studio Kullanıcı arabirimi içinde olması gerekmez), sağ alt köşedeki Damlalık aracını kullanarak değerini yakalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b820-257">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="6b820-258">Ayrıca renk seçicinin alt kısmına kaydırıcıyı taşıyarak bir rengin saydamlığını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b820-258">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="6b820-259">Bunun yapılması, RGBA biçimi geçirgenliği temsil ettiğinden, renk değerlerini RGBA değerlerine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="6b820-259">Doing so changes color values to RGBA values because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="6b820-260">Bir renk seçtikten sonra, ENTER tuşuna basın ve ardından *site. css* dosyasındaki arka plan rengi girişini tamamlamaya yönelik bir noktalı virgül yazın.</span><span class="sxs-lookup"><span data-stu-id="6b820-260">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="6b820-261">Sayfa denetçisi güncelleştirme çubuğu</span><span class="sxs-lookup"><span data-stu-id="6b820-261">The Page Inspector Update Bar</span></span>

<span data-ttu-id="6b820-262">Sayfa denetçisi, *site. css* dosyasındaki (veya uygulamadaki herhangi bir dosya) yapılan değişikliği hemen algılar ve bir güncelleştirme çubuğunda bir uyarı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6b820-262">Page Inspector immediately detects the change to the *Site.css* file (or to any file in the application) and displays an alert in an update bar.</span></span>

![Güncelleştirme çubuğu](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

<span data-ttu-id="6b820-264">Tüm dosyalarınızı kaydetmek ve sayfa denetçisi tarayıcısını yenilemek için CTRL + ALT + ENTER tuşlarına basın veya güncelleştirme çubuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b820-264">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="6b820-265">Vurgu renginizdeki değişiklik tarayıcıda görünür:</span><span class="sxs-lookup"><span data-stu-id="6b820-265">The change in the highlight color appears in the browser:</span></span>

![Vurgu rengi değişti](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a><span data-ttu-id="6b820-267">Sayfa denetçisi tarayıcısını doğrudan Visual Studio ortamının içinden yenileyenizi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6b820-267">Notice that you conveniently refreshed the Page Inspector browser right from within the Visual Studio environment.</span></span> <span data-ttu-id="6b820-268">Dış tarayıcı yerine sayfa denetçisi kullanmak, Web uygulamalarınızı geliştirirken düzenleyicide kalmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b820-268">Using Page Inspector instead of an external browser lets you stay in the editor when you develop your web applications.</span></span>

## <a name="see-also"></a><span data-ttu-id="6b820-269">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="6b820-269">See Also</span></span>

<span data-ttu-id="6b820-270">[Sayfa denetçisi Ile tanışın](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 Videosu)</span><span class="sxs-lookup"><span data-stu-id="6b820-270">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 video)</span></span>

<span data-ttu-id="6b820-271">[Sayfa denetçisi hata iletileri](https://go.microsoft.com/?linkid=9813062) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="6b820-271">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
