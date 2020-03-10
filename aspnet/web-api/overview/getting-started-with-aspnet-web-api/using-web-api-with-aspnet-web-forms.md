---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: ASP.NET Web Forms-ASP.NET 4. x ile Web API 'sini kullanma
author: MikeWasson
description: ASP.NET 4. x için ASP.NET Forms uygulamasına Web API 'SI eklemek üzere kod adım adım ile öğretici
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556779"
---
# <a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="c417f-103">ASP.NET Web Forms ile Web API Kullanma</span><span class="sxs-lookup"><span data-stu-id="c417f-103">Using Web API with ASP.NET Web Forms</span></span>

<span data-ttu-id="c417f-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c417f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c417f-105">Bu öğretici, ASP.NET 4. x içindeki geleneksel bir ASP.NET Web Forms uygulamasına Web API 'SI ekleme adımlarında size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="c417f-105">This tutorial walks you through the steps to add Web API to a traditional ASP.NET Web Forms application in ASP.NET 4.x.</span></span> 

## <a name="overview"></a><span data-ttu-id="c417f-106">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="c417f-106">Overview</span></span>

<span data-ttu-id="c417f-107">ASP.NET Web API 'SI ASP.NET MVC ile paketlense de, Web API 'sini geleneksel bir ASP.NET Web Forms uygulamasına eklemek kolaydır.</span><span class="sxs-lookup"><span data-stu-id="c417f-107">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span>

<span data-ttu-id="c417f-108">Web API 'sini bir Web Forms uygulamasında kullanmak için iki ana adım vardır:</span><span class="sxs-lookup"><span data-stu-id="c417f-108">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="c417f-109">**Apicontroller** sınıfından türetilen BIR Web API denetleyicisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c417f-109">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="c417f-110">**Uygulama\_start** yöntemine bir yol tablosu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c417f-110">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="c417f-111">Web Forms projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c417f-111">Create a Web Forms Project</span></span>

<span data-ttu-id="c417f-112">Visual Studio 'Yu başlatın ve **Başlangıç** sayfasından **Yeni proje** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c417f-112">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="c417f-113">Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c417f-113">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="c417f-114">**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="c417f-114">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="c417f-115">**Görsel C#** bölümünde **Web**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="c417f-115">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="c417f-116">Proje şablonları listesinde **ASP.NET Web Forms uygulama**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="c417f-116">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="c417f-117">Proje için bir ad girin ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c417f-117">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="c417f-118">Modeli ve denetleyiciyi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c417f-118">Create the Model and Controller</span></span>

<span data-ttu-id="c417f-119">Bu [öğretici, başlangıç öğreticisiyle](tutorial-your-first-web-api.md) aynı model ve denetleyici sınıflarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="c417f-119">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="c417f-120">İlk olarak, bir model sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c417f-120">First, add a model class.</span></span> <span data-ttu-id="c417f-121">**Çözüm Gezgini**, projeye sağ tıklayın ve **Sınıf Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c417f-121">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="c417f-122">Sınıf ürününü adlandırın ve aşağıdaki uygulamayı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c417f-122">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="c417f-123">Sonra, projeye bir Web API denetleyicisi ekleyin. bir *Denetleyici* , Web API 'SI için http isteklerini işleyen nesnedir.</span><span class="sxs-lookup"><span data-stu-id="c417f-123">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="c417f-124">**Çözüm Gezgini**, projeye sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c417f-124">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="c417f-125">**Yeni öğe Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c417f-125">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="c417f-126">**Yüklü şablonlar**altında, **görsel C#**  ' i genişletin ve **Web**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="c417f-126">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="c417f-127">Ardından, şablonlar listesinden **Web API denetleyici sınıfı**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="c417f-127">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="c417f-128">Denetleyiciyi "ProductsController" olarak adlandırın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c417f-128">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="c417f-129">**Yeni öğe ekleme** sihirbazı, ProductsController.cs adlı bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c417f-129">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="c417f-130">Sihirbazın dahil olduğu yöntemleri silin ve aşağıdaki yöntemleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c417f-130">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="c417f-131">Bu denetleyicideki kod hakkında daha fazla bilgi için bkz. [Başlangıç](tutorial-your-first-web-api.md) öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="c417f-131">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="c417f-132">Yönlendirme bilgilerini ekle</span><span class="sxs-lookup"><span data-stu-id="c417f-132">Add Routing Information</span></span>

<span data-ttu-id="c417f-133">Daha sonra, &quot;/api/Products/&quot; formundaki URI 'Lerin denetleyiciye yönlendirilmesi için bir URI yolu ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="c417f-133">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="c417f-134">**Çözüm Gezgini**' de, Global. asax dosyasına çift tıklayarak Global.asax.cs dosya arkasındaki kodu açın.</span><span class="sxs-lookup"><span data-stu-id="c417f-134">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="c417f-135">Aşağıdaki **using** ifadesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c417f-135">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="c417f-136">Ardından aşağıdaki kodu **uygulama\_başlangıç** yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c417f-136">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="c417f-137">Yönlendirme tabloları hakkında daha fazla bilgi için bkz. [ASP.NET Web API 'de yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="c417f-137">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="c417f-138">Istemci tarafı AJAX ekleme</span><span class="sxs-lookup"><span data-stu-id="c417f-138">Add Client-Side AJAX</span></span>

<span data-ttu-id="c417f-139">Bu, istemcilerin erişebileceği bir Web API 'SI oluşturmanız için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="c417f-139">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="c417f-140">Şimdi de API 'YI çağırmak için jQuery kullanan bir HTML sayfası ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="c417f-140">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="c417f-141">Ana sayfanızın (örneğin, *site. Master*) `ID="HeadContent"`bir `ContentPlaceHolder` içerdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="c417f-141">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="c417f-142">Default. aspx dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="c417f-142">Open the file Default.aspx.</span></span> <span data-ttu-id="c417f-143">Ana İçerik bölümündeki ortak metni gösterildiği gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c417f-143">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="c417f-144">Sonra, `HeaderContent` bölümünde jQuery kaynak dosyasına bir başvuru ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c417f-144">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="c417f-145">Note: dosya **Çözüm Gezgini** ' den kod Düzenleyicisi penceresine sürükleyip bırakarak betik başvurusunu kolayca ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c417f-145">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="c417f-146">JQuery betiği etiketinin altında aşağıdaki betik bloğunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c417f-146">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="c417f-147">Belge yüklendiğinde, bu betik API/ürün&quot;&quot;bir AJAX isteği yapar.</span><span class="sxs-lookup"><span data-stu-id="c417f-147">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="c417f-148">İstek JSON biçimindeki ürünlerin bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="c417f-148">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="c417f-149">Betik, ürün bilgilerini HTML tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="c417f-149">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="c417f-150">Uygulamayı çalıştırdığınızda, şöyle görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="c417f-150">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
