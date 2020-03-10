---
uid: visual-studio/overview/2013/using-browser-link
title: Visual Studio 2013 'de tarayıcı bağlantısı kullanılıyor | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 723a38de4569b0bb58817c70aabb84fef8e19591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622908"
---
# <a name="using-browser-link-in-visual-studio-2013"></a><span data-ttu-id="d8529-102">Visual Studio 2013 'de tarayıcı bağlantısı kullanma</span><span class="sxs-lookup"><span data-stu-id="d8529-102">Using Browser Link in Visual Studio 2013</span></span>

<span data-ttu-id="d8529-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d8529-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="d8529-104">Tarayıcı bağlantısı, geliştirme ortamı ile bir veya daha fazla Web tarayıcısı arasında bir iletişim kanalı oluşturan Visual Studio 2013 yeni bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="d8529-104">Browser Link is a new feature in Visual Studio 2013 that creates a communication channel between the development environment and one or more web browsers.</span></span> <span data-ttu-id="d8529-105">Tarayıcı bağlantısını, Web uygulamanızı birden çok tarayıcıda tek seferde yenilemek için kullanabilirsiniz. Bu, tarayıcılar arası testler için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="d8529-105">You can use Browser Link to refresh your web application in several browsers at once, which is useful for cross-browser testing.</span></span>

- [<span data-ttu-id="d8529-106">Tarayıcı yenileme</span><span class="sxs-lookup"><span data-stu-id="d8529-106">Browser Refresh</span></span>](#browser-refresh)
- [<span data-ttu-id="d8529-107">Tarayıcı bağlantısı panosunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="d8529-107">Viewing the Browser Link Dashboard</span></span>](#dashboard)
- [<span data-ttu-id="d8529-108">Statik HTML dosyaları için tarayıcı bağlantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d8529-108">Enabling Browser Link for Static HTML Files</span></span>](#static-html)
- [<span data-ttu-id="d8529-109">Tarayıcı bağlantısı devre dışı bırakılıyor</span><span class="sxs-lookup"><span data-stu-id="d8529-109">Disabling Browser Link</span></span>](#disabling)
- [<span data-ttu-id="d8529-110">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="d8529-110">How Does It Work?</span></span>](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a><span data-ttu-id="d8529-111">Tarayıcı yenileme</span><span class="sxs-lookup"><span data-stu-id="d8529-111">Browser Refresh</span></span>

<span data-ttu-id="d8529-112">Tarayıcı yenileme ile, tarayıcı bağlantısı aracılığıyla Visual Studio 'ya bağlı birden çok tarayıcıyı yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8529-112">With Browser Refresh, you can refresh multiple browsers that are connected to Visual Studio through Browser Link.</span></span>

<span data-ttu-id="d8529-113">Tarayıcı yenilemeyi kullanmak için, önce proje şablonlarından birini kullanarak bir ASP.NET uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d8529-113">To use Browser Refresh, first create an ASP.NET application, using any of the project templates.</span></span> <span data-ttu-id="d8529-114">F5 tuşuna basarak veya araç çubuğundaki ok simgesine tıklayarak uygulamada hata ayıklayın:</span><span class="sxs-lookup"><span data-stu-id="d8529-114">Debug the application by pressing F5 or clicking the arrow icon in the toolbar:</span></span>

![](using-browser-link/_static/image1.png)

<span data-ttu-id="d8529-115">Ayrıca, hata ayıklama için belirli bir tarayıcı seçmek üzere açılan menüyü de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8529-115">You can also use the dropdown to select a specific browser for debugging.</span></span>

![](using-browser-link/_static/image2.png)

<span data-ttu-id="d8529-116">Birden çok tarayıcıyla hata ayıklamak için, **Ile araştır**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d8529-116">To debug with multiple browsers, select **Browse With**.</span></span> <span data-ttu-id="d8529-117">**Ile araştır** iletişim kutusunda, birden fazla tarayıcı seçmek için CTRL tuşunu basılı tutun.</span><span class="sxs-lookup"><span data-stu-id="d8529-117">In the **Browse With** dialog, hold down the CTRL key to select more than one browser.</span></span> <span data-ttu-id="d8529-118">Seçili tarayıcılarla hata ayıklamak için, **Gözden** geçirme ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8529-118">Click **Browse** to debug with the selected browsers.</span></span> <span data-ttu-id="d8529-119">Tarayıcı bağlantısı, Visual Studio dışında bir tarayıcı başlattığınızda ve uygulama URL 'sine gittiğinizde da geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d8529-119">Browser Link also works if you launch a browser from outside Visual Studio and navigate to the application URL.</span></span>

![](using-browser-link/_static/image3.png)

<span data-ttu-id="d8529-120">Tarayıcı bağlantı denetimleri, dairesel ok simgesiyle açılan listede bulunur.</span><span class="sxs-lookup"><span data-stu-id="d8529-120">The Browser Link controls are located in the dropdown with the circular arrow icon.</span></span> <span data-ttu-id="d8529-121">Ok simgesi **Yenile** düğmesidir.</span><span class="sxs-lookup"><span data-stu-id="d8529-121">The arrow icon is the **Refresh** button.</span></span>

![](using-browser-link/_static/image4.png)

<span data-ttu-id="d8529-122">Hangi tarayıcıların bağlı olduğunu görmek için, hata ayıklama sırasında fareyi **Yenile** düğmesinin üzerine getirin.</span><span class="sxs-lookup"><span data-stu-id="d8529-122">To see which browsers are connected, hover the mouse over the **Refresh** button while debugging.</span></span> <span data-ttu-id="d8529-123">Bağlı tarayıcılar bir araç Ipucu penceresinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d8529-123">The connected browsers are shown in a ToolTip window.</span></span>

![](using-browser-link/_static/image5.png)

<span data-ttu-id="d8529-124">Bağlı tarayıcıları yenilemek için **Yenile** düğmesine tıklayın veya CTRL + ALT + ENTER tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="d8529-124">To refresh the connected browsers, click the **Refresh** button or press CTRL+ALT+ENTER.</span></span> <span data-ttu-id="d8529-125">Örneğin, aşağıdaki ekran görüntüsünde MVC 5 proje şablonunu kullanarak oluşturduğum bir ASP.NET projesi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d8529-125">For example, the following screenshot shows an ASP.NET project, which I created using the MVC 5 project template.</span></span> <span data-ttu-id="d8529-126">En üstte iki tarayıcıda çalışan uygulamayı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8529-126">You can see the application running in two browsers at the top.</span></span> <span data-ttu-id="d8529-127">En altta, proje Visual Studio 'da açıktır.</span><span class="sxs-lookup"><span data-stu-id="d8529-127">At the bottom, the project is open in Visual Studio.</span></span>

![](using-browser-link/_static/image6.png)

<span data-ttu-id="d8529-128">Visual Studio 'da ana sayfa için &lt;H1&gt; başlığını değiştirdim:</span><span class="sxs-lookup"><span data-stu-id="d8529-128">In Visual Studio, I changed the &lt;h1&gt; heading for the home page:</span></span>

![](using-browser-link/_static/image7.png)

<span data-ttu-id="d8529-129">**Yenile** düğmesine tıkladığımda değişiklik her iki tarayıcı penceresinde de görünüyor:</span><span class="sxs-lookup"><span data-stu-id="d8529-129">When I clicked the **Refresh** button, the change appeared in both browser windows:</span></span>

![](using-browser-link/_static/image8.png)

<span data-ttu-id="d8529-130">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="d8529-130">**Notes**</span></span>

- <span data-ttu-id="d8529-131">Tarayıcı bağlantısını etkinleştirmek için, projenin Web. config dosyasındaki [&lt;derleme&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) öğesinde `debug=true` ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d8529-131">To enable Browser Link, set `debug=true` in the [&lt;compilation&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) element in the project's Web.config file.</span></span>
- <span data-ttu-id="d8529-132">Uygulamanın localhost üzerinde çalışıyor olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8529-132">The application must be running on localhost.</span></span>
- <span data-ttu-id="d8529-133">Uygulamanın .NET 4,0 veya üstünü hedeflemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8529-133">The application must target .NET 4.0 or later.</span></span>

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a><span data-ttu-id="d8529-134">Tarayıcı bağlantısı panosunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="d8529-134">Viewing the Browser Link Dashboard</span></span>

<span data-ttu-id="d8529-135">Tarayıcı bağlantısı panosu, tarayıcı bağlantısı bağlantıları hakkında bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="d8529-135">The Browser Link dashboard shows information about the Browser Link connections.</span></span> <span data-ttu-id="d8529-136">Panoyu görüntülemek için tarayıcı bağlantısı açılan menüsünü seçin ( **Yenile** düğmesinin yanındaki küçük ok).</span><span class="sxs-lookup"><span data-stu-id="d8529-136">To view the dashboard, select the Browser Link dropdown menu (the small arrow next to the **Refresh** button).</span></span> <span data-ttu-id="d8529-137">Ardından **tarayıcı bağlantısı panosu**' na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8529-137">Then click **Browser Link Dashboard**.</span></span>

![](using-browser-link/_static/image9.png)

<span data-ttu-id="d8529-138">Pano, bağlı tarayıcıları ve her tarayıcının gezindiği URL 'YI listeler.</span><span class="sxs-lookup"><span data-stu-id="d8529-138">The dashboard lists the connected Browsers and the URL to which each browser has navigated.</span></span>

![](using-browser-link/_static/image10.png)

<span data-ttu-id="d8529-139">**Önkoşullar** bölümünde, bu proje Için tarayıcı bağlantısını etkinleştirmek üzere gereken adımlar gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d8529-139">The **Prerequisites** section shows any steps needed to enable Browser Link for that project.</span></span> <span data-ttu-id="d8529-140">Örneğin, aşağıdaki ekran görüntüsünde, Web. config dosyasında "Debug" false olarak ayarlanmış bir proje gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d8529-140">For example, the following screenshot shows a project where "debug" is set to false in the Web.config file.</span></span>

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a><span data-ttu-id="d8529-141">Statik HTML dosyaları için tarayıcı bağlantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d8529-141">Enabling Browser Link for Static HTML Files</span></span>

<span data-ttu-id="d8529-142">Statik HTML dosyaları için tarayıcı bağlantısını etkinleştirmek üzere, Web. config dosyanıza aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d8529-142">To enable Browser Link for static HTML files, add the following to your Web.config file.</span></span>

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

<span data-ttu-id="d8529-143">Performans nedenleriyle, projenizi yayımladığınızda bu ayarı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d8529-143">For performance reasons, remove this setting when you publish your project.</span></span>

<a id="disabling"></a>
## <a name="disabling-browser-link"></a><span data-ttu-id="d8529-144">Tarayıcı bağlantısı devre dışı bırakılıyor</span><span class="sxs-lookup"><span data-stu-id="d8529-144">Disabling Browser Link</span></span>

<span data-ttu-id="d8529-145">Tarayıcı bağlantısı varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="d8529-145">Browser Link is enabled by default.</span></span> <span data-ttu-id="d8529-146">Devre dışı bırakmak için birkaç yol vardır:</span><span class="sxs-lookup"><span data-stu-id="d8529-146">There are several ways to disable it:</span></span>

- <span data-ttu-id="d8529-147">Tarayıcı bağlantısı açılan menüsünde, **tarayıcı bağlantısını etkinleştir**onay kutusunun işaretini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d8529-147">In the Browser Link dropdown menu, uncheck **Enable Browser Link**.</span></span> 

    ![](using-browser-link/_static/image12.png)
- <span data-ttu-id="d8529-148">Web. config dosyasında, appSettings bölümüne "vs: EnableBrowserLink" adlı bir anahtarı "false" değeri ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d8529-148">In the Web.config file, add a key named "vs:EnableBrowserLink" with the value "false" in the appSettings section.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- <span data-ttu-id="d8529-149">Web. config dosyasında, hata ayıkla ' yı false olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d8529-149">In the Web.config file, set debug to false.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a><span data-ttu-id="d8529-150">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="d8529-150">How Does It Work?</span></span>

<span data-ttu-id="d8529-151">Tarayıcı bağlantısı, Visual Studio ile tarayıcı arasında bir iletişim kanalı oluşturmak için [SignalR](../../../signalr/index.md) kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8529-151">Browser Link uses [SignalR](../../../signalr/index.md) to create a communication channel between Visual Studio and the browser.</span></span> <span data-ttu-id="d8529-152">Tarayıcı bağlantısı etkinleştirildiğinde, Visual Studio birden çok istemcinin (tarayıcının) bağlanabileceği bir SignalR sunucusu işlevi görür.</span><span class="sxs-lookup"><span data-stu-id="d8529-152">When Browser Link is enabled, Visual Studio acts as a SignalR server that multiple clients (browsers) can connect to.</span></span> <span data-ttu-id="d8529-153">Tarayıcı bağlantısı, ASP.NET ile bir HTTP modülünü de kaydeder.</span><span class="sxs-lookup"><span data-stu-id="d8529-153">Browser Link also registers an HTTP module with ASP.NET.</span></span> <span data-ttu-id="d8529-154">Bu modül, sunucudan her sayfa isteğine özel &lt;betiği&gt; başvurularını çıkarır.</span><span class="sxs-lookup"><span data-stu-id="d8529-154">This module injects special &lt;script&gt; references into every page request from the server.</span></span> <span data-ttu-id="d8529-155">Tarayıcıda "kaynağı görüntüle" seçeneğini belirleyerek betik başvurularını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8529-155">You can see the script references by selecting "View source" in the browser.</span></span>

![](using-browser-link/_static/image13.png)

<span data-ttu-id="d8529-156">Kaynak dosyalarınız değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="d8529-156">Your source files are not modified.</span></span> <span data-ttu-id="d8529-157">HTTP modülü betik başvurularını dinamik olarak çıkarır.</span><span class="sxs-lookup"><span data-stu-id="d8529-157">The HTTP module injects the script references dynamically.</span></span>

<span data-ttu-id="d8529-158">Tarayıcı tarafı kodu tüm JavaScript olduğundan, herhangi bir tarayıcı eklentisi gerekmeden, [SignalR 'nin desteklediği](../../../signalr/overview/getting-started/supported-platforms.md)tüm tarayıcılarda çalışıyor olur.</span><span class="sxs-lookup"><span data-stu-id="d8529-158">Because the browser-side code is all JavaScript, it works on all browsers that [SignalR supports](../../../signalr/overview/getting-started/supported-platforms.md), without requiring any browser plug-in.</span></span>
