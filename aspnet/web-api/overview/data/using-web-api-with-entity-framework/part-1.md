---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: Entity Framework 6 ile Web API 2 kullanma | Microsoft Docs
author: MikeWasson
description: Bu öğretici, ASP.NET Web API arka ucu ile bir Web uygulaması oluşturma hakkında temel bilgileri öğretir. Öğretici, veri düzenleme için Entity Framework 6 kullanır...
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622481"
---
# <a name="using-web-api-2-with-entity-framework-6"></a><span data-ttu-id="06b8d-104">Web API 2’yi Entity Framework 6 ile Kullanma</span><span class="sxs-lookup"><span data-stu-id="06b8d-104">Using Web API 2 with Entity Framework 6</span></span>

[<span data-ttu-id="06b8d-105">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="06b8d-105">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

> <span data-ttu-id="06b8d-106">Bu öğretici, ASP.NET Web API arka ucu ile bir Web uygulaması oluşturma hakkında temel bilgileri öğretir.</span><span class="sxs-lookup"><span data-stu-id="06b8d-106">This tutorial teaches you the basics of creating a web application with an ASP.NET Web API back end.</span></span> <span data-ttu-id="06b8d-107">Öğretici, veri katmanı için Entity Framework 6 ve istemci tarafı JavaScript uygulaması için altını gizleme. js ' yi kullanır.</span><span class="sxs-lookup"><span data-stu-id="06b8d-107">The tutorial uses Entity Framework 6 for the data layer, and Knockout.js for the client-side JavaScript application.</span></span> <span data-ttu-id="06b8d-108">Öğreticide Ayrıca uygulamanın Azure App Service Web Apps nasıl dağıtılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="06b8d-108">The tutorial also shows how to deploy the app to Azure App Service Web Apps.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="06b8d-109">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="06b8d-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="06b8d-110">Web API 2.1</span><span class="sxs-lookup"><span data-stu-id="06b8d-110">Web API 2.1</span></span>
> - <span data-ttu-id="06b8d-111">Visual Studio 2017 (Visual Studio 2017 [buraya](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)indirin)</span><span class="sxs-lookup"><span data-stu-id="06b8d-111">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="06b8d-112">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="06b8d-112">Entity Framework 6</span></span>
> - <span data-ttu-id="06b8d-113">.NET 4.7</span><span class="sxs-lookup"><span data-stu-id="06b8d-113">.NET 4.7</span></span>
> - <span data-ttu-id="06b8d-114">[Altını gizleme. js](http://knockoutjs.com/) 3,1</span><span class="sxs-lookup"><span data-stu-id="06b8d-114">[Knockout.js](http://knockoutjs.com/) 3.1</span></span>

<span data-ttu-id="06b8d-115">Bu öğretici, arka uç veritabanını işleyen bir Web uygulaması oluşturmak için Entity Framework 6 ile ASP.NET Web API 2 kullanır.</span><span class="sxs-lookup"><span data-stu-id="06b8d-115">This tutorial uses ASP.NET Web API 2 with Entity Framework 6 to create a web application that manipulates a back-end database.</span></span> <span data-ttu-id="06b8d-116">Burada oluşturacağınız uygulamanın ekran görüntüsü gösterilir.</span><span class="sxs-lookup"><span data-stu-id="06b8d-116">Here is a screen shot of the application that you will create.</span></span>

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

<span data-ttu-id="06b8d-117">Uygulama, tek sayfalı uygulama (SPA) tasarımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="06b8d-117">The app uses a single-page application (SPA) design.</span></span> <span data-ttu-id="06b8d-118">"Tek sayfalı uygulama", tek bir HTML sayfası yükleyen bir Web uygulaması için genel bir terimdir ve sonra yeni sayfalar yüklemek yerine sayfayı dinamik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="06b8d-118">"Single-page application" is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="06b8d-119">İlk sayfa yüklendikten sonra uygulama, AJAX istekleri aracılığıyla sunucusuyla iletişim kuran bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="06b8d-119">After the initial page load, the app talks with the server through AJAX requests.</span></span> <span data-ttu-id="06b8d-120">AJAX istekleri, uygulamanın kullanıcı arabirimini güncelleştirmek için kullandığı JSON verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="06b8d-120">The AJAX requests return JSON data, which the app uses to update the UI.</span></span>

<span data-ttu-id="06b8d-121">AJAX yeni değil, ancak bugün büyük bir Gelişmiş SPA uygulaması oluşturmayı ve bakımını kolaylaştıran JavaScript çerçeveleri vardır.</span><span class="sxs-lookup"><span data-stu-id="06b8d-121">AJAX isn't new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="06b8d-122">Bu öğretici, [altını gizleme. js](http://knockoutjs.com/)kullanır, ancak herhangi bir JavaScript istemci çerçevesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06b8d-122">This tutorial uses [Knockout.js](http://knockoutjs.com/), but you can use any JavaScript client framework.</span></span>

<span data-ttu-id="06b8d-123">Bu uygulama için ana yapı taşları aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="06b8d-123">Here are the main building blocks for this app:</span></span>

- <span data-ttu-id="06b8d-124">ASP.NET MVC HTML sayfasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="06b8d-124">ASP.NET MVC creates the HTML page.</span></span>
- <span data-ttu-id="06b8d-125">ASP.NET Web API 'SI AJAX isteklerini işler ve JSON verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="06b8d-125">ASP.NET Web API handles the AJAX requests and returns JSON data.</span></span>
- <span data-ttu-id="06b8d-126">Altını gizleme. js verileri-HTML öğelerini JSON verilerine bağlar.</span><span class="sxs-lookup"><span data-stu-id="06b8d-126">Knockout.js data-binds the HTML elements to the JSON data.</span></span>
- <span data-ttu-id="06b8d-127">Entity Framework veritabanı ile konuşuyor.</span><span class="sxs-lookup"><span data-stu-id="06b8d-127">Entity Framework talks to the database.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="06b8d-128">Bkz. Azure 'da çalışan bu uygulama</span><span class="sxs-lookup"><span data-stu-id="06b8d-128">See this app running on Azure</span></span>

<span data-ttu-id="06b8d-129">Canlı bir Web uygulaması olarak çalışan tamamlanmış siteyi görmek istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="06b8d-129">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="06b8d-130">Aşağıdaki düğmeyi seçerek uygulamanın tüm sürümünü Azure hesabınıza dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06b8d-130">You can deploy a complete version of the app to your Azure account by selecting the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

<span data-ttu-id="06b8d-131">Bu çözümü Azure 'a dağıtmak için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="06b8d-131">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="06b8d-132">Henüz bir hesabınız yoksa, aşağıdaki seçeneklere sahip olursunuz:</span><span class="sxs-lookup"><span data-stu-id="06b8d-132">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="06b8d-133">[Ücretsiz bir Azure hesabı açarak](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) ücretli Azure hizmetlerini denemek için kullanabileceğiniz krediler edinin ve hatta kullanıldıktan sonra bile hesabı tutabilir ve ücretsiz Azure hizmetlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06b8d-133">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="06b8d-134">[MSDN abonesi avantajlarınızı etkinleştirin](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN aboneliğiniz, ücretli Azure hizmetleri için kullanabileceğiniz her ay krediler sunar.</span><span class="sxs-lookup"><span data-stu-id="06b8d-134">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="06b8d-135">Projeyi oluşturma</span><span class="sxs-lookup"><span data-stu-id="06b8d-135">Create the project</span></span>

<span data-ttu-id="06b8d-136">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="06b8d-136">Open Visual Studio.</span></span> <span data-ttu-id="06b8d-137">**Dosya** menüsünde **Yeni**' yi ve ardından **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-137">From the **File** menu, select **New**, then select **Project**.</span></span> <span data-ttu-id="06b8d-138">(Veya başlangıç sayfasında **Yeni proje** ' yi seçin.)</span><span class="sxs-lookup"><span data-stu-id="06b8d-138">(Or select **New Project** on the Start page.)</span></span>

<span data-ttu-id="06b8d-139">**Yeni proje** iletişim kutusunda sol bölmedeki Web ' i ve **ASP.NET Web uygulaması ' nı (.NET Framework)** ortadaki bölmedeki **Web** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-139">In the **New Project** dialog, select **Web** in the left pane and **ASP.NET Web Application (.NET Framework)** in the middle pane.</span></span> <span data-ttu-id="06b8d-140">Proje **Bookservice** 'i adlandırın ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-140">Name the project **BookService** and select **OK**.</span></span>

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

<span data-ttu-id="06b8d-141">**Yeni ASP.NET projesi** Iletişim kutusunda **Web API** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-141">In the **New ASP.NET Project** dialog, select the **Web API** template.</span></span>

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

<span data-ttu-id="06b8d-142">Projeyi oluşturmak için **Tamam**'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-142">Select **OK** to create the project.</span></span>

## <a name="configure-azure-settings-optional"></a><span data-ttu-id="06b8d-143">Azure ayarlarını yapılandırma (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="06b8d-143">Configure Azure settings (optional)</span></span>

<span data-ttu-id="06b8d-144">Projeyi oluşturduktan sonra dilediğiniz zaman Azure App Service Web Apps dağıtmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06b8d-144">After you create the project, you can choose to deploy to Azure App Service Web Apps at any time.</span></span> 

1. <span data-ttu-id="06b8d-145">Çözüm Gezgini, projenize sağ tıklayın ve **Yayımla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-145">In Solution Explorer, right-click on your project and select **Publish**.</span></span>

2. <span data-ttu-id="06b8d-146">Görüntülenen pencerede **Başlat**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-146">In the window that appears, select **Start**.</span></span> <span data-ttu-id="06b8d-147">**Bir Yayımla hedefi seç** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="06b8d-147">The **Pick a publish target** dialog box appears.</span></span>

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. <span data-ttu-id="06b8d-148">**Profil oluştur**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-148">Select **Create Profile**.</span></span> <span data-ttu-id="06b8d-149">**App Service oluştur** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="06b8d-149">The **Create App Service** dialog box appears.</span></span>

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   <span data-ttu-id="06b8d-150">Varsayılanları kabul edin veya uygulama adı, kaynak grubu, barındırma planı, Azure aboneliği ve coğrafi bölge için farklı değerler girin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-150">Accept the defaults, or enter different values for the application name, resource group, hosting plan, Azure subscription, and geographical region.</span></span> 

4. <span data-ttu-id="06b8d-151">**SQL veritabanı oluştur**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-151">Select **Create a SQL database**.</span></span> <span data-ttu-id="06b8d-152">**SQL Server Yapılandır** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="06b8d-152">The **Configure SQL Server** dialog box appears.</span></span> 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   <span data-ttu-id="06b8d-153">Varsayılanları kabul edin veya farklı değerler girin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-153">Accept the defaults or enter different values.</span></span> <span data-ttu-id="06b8d-154">Yeni veritabanınız için bir **Yönetici Kullanıcı adı** ve **yönetici parolası** girin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-154">Enter an **Administrator Username** and **Administrator Password** for your new database.</span></span> <span data-ttu-id="06b8d-155">İşiniz bittiğinde **Tamam ' ı** seçin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-155">Select **OK** when you're done.</span></span> <span data-ttu-id="06b8d-156">**App Service oluştur** sayfası yeniden görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="06b8d-156">The **Create App Service** page reappears.</span></span>

5. <span data-ttu-id="06b8d-157">Profilinizi oluşturmak için **Oluştur** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="06b8d-157">Select **Create** to create your profile.</span></span> <span data-ttu-id="06b8d-158">Sağ alt köşede, dağıtımın devam ettiğini belirten bir ileti görünür.</span><span class="sxs-lookup"><span data-stu-id="06b8d-158">A message appears in the lower-right corner indicating that deployment is in progress.</span></span> <span data-ttu-id="06b8d-159">Kısa bir süre sonra, **Yayımla** penceresi yeniden görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="06b8d-159">After a short while, the **Publish** window reappears.</span></span>

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    <span data-ttu-id="06b8d-160">Uygulamayı dağıtmak için oluşturduğunuz profil artık kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="06b8d-160">The profile you created to deploy the app is now available.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="06b8d-161">Next</span><span class="sxs-lookup"><span data-stu-id="06b8d-161">Next</span></span>](part-2.md)
