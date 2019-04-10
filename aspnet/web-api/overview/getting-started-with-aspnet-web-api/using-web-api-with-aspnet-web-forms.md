---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: ASP.NET Web Forms ile - ASP.NET Web API kullanma 4.x
author: MikeWasson
description: Kodla Web API'si için bir ASP.NET Forms uygulaması için ASP.NET eklemek için adım adım öğretici 4.x
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59422583"
---
# <a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="61c49-103">ASP.NET Web Forms ile Web API Kullanma</span><span class="sxs-lookup"><span data-stu-id="61c49-103">Using Web API with ASP.NET Web Forms</span></span>

<span data-ttu-id="61c49-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="61c49-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="61c49-105">Bu öğreticide, geleneksel bir ASP.NET Web Forms uygulaması ASP.NET Web API eklemek için adım adım anlatılmaktadır 4.x.</span><span class="sxs-lookup"><span data-stu-id="61c49-105">This tutorial walks you through the steps to add Web API to a traditional ASP.NET Web Forms application in ASP.NET 4.x.</span></span> 

## <a name="overview"></a><span data-ttu-id="61c49-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="61c49-106">Overview</span></span>

<span data-ttu-id="61c49-107">ASP.NET Web API, ASP.NET MVC ile paketlenmiştir olsa da, Web API'si için geleneksel bir ASP.NET Web Forms uygulaması eklemek kolay bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="61c49-107">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span>

<span data-ttu-id="61c49-108">Bir Web Forms uygulaması'nda Web API'sini kullanmak için iki ana adım vardır:</span><span class="sxs-lookup"><span data-stu-id="61c49-108">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="61c49-109">Türetilen bir Web API denetleyicisi ekleme **ApiController** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="61c49-109">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="61c49-110">Bir rota tablosuna ekleme **uygulama\_Başlat** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="61c49-110">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="61c49-111">Web Forms projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="61c49-111">Create a Web Forms Project</span></span>

<span data-ttu-id="61c49-112">Visual Studio'yu başlatın ve seçin **yeni proje** gelen **Başlat** sayfası.</span><span class="sxs-lookup"><span data-stu-id="61c49-112">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="61c49-113">Veya **dosya** menüsünde **yeni** ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="61c49-113">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="61c49-114">İçinde **şablonları** bölmesinde **yüklü şablonlar** genişletin **Visual C#** düğümü.</span><span class="sxs-lookup"><span data-stu-id="61c49-114">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="61c49-115">Altında **Visual C#** seçin **Web**.</span><span class="sxs-lookup"><span data-stu-id="61c49-115">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="61c49-116">Proje şablonları listesinde seçin **ASP.NET Web Forms uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="61c49-116">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="61c49-117">Proje için bir ad girin ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="61c49-117">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="61c49-118">Model ve denetleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="61c49-118">Create the Model and Controller</span></span>

<span data-ttu-id="61c49-119">Bu öğreticide aynı model ve denetleyici sınıflar olarak [Başlarken](tutorial-your-first-web-api.md) öğretici.</span><span class="sxs-lookup"><span data-stu-id="61c49-119">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="61c49-120">İlk olarak, bir model sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="61c49-120">First, add a model class.</span></span> <span data-ttu-id="61c49-121">İçinde **Çözüm Gezgini**, projeye sağ tıklayıp seçin **sınıfı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="61c49-121">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="61c49-122">' % S'sınıfı ürün adı ve aşağıdaki uygulama ekleyin:</span><span class="sxs-lookup"><span data-stu-id="61c49-122">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="61c49-123">Ardından, bir Web API denetleyicisi proje, A ekleyin. *denetleyicisi* Web API'si için HTTP isteklerini işleyen nesne.</span><span class="sxs-lookup"><span data-stu-id="61c49-123">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="61c49-124">İçinde **Çözüm Gezgini**, projeye sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61c49-124">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="61c49-125">Seçin **Add New Item**.</span><span class="sxs-lookup"><span data-stu-id="61c49-125">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="61c49-126">Altında **yüklü şablonlar**, genişletme **Visual C#** seçip **Web**.</span><span class="sxs-lookup"><span data-stu-id="61c49-126">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="61c49-127">Şablonlar listesinden seçip **Web API denetleyici sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="61c49-127">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="61c49-128">Denetleyici "ProductsController" adını verin ve tıklayın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="61c49-128">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="61c49-129">**Yeni Öğe Ekle** Sihirbazı ProductsController.cs adlı bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="61c49-129">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="61c49-130">Sihirbaz dahil yöntemleri silin ve aşağıdaki yöntemleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="61c49-130">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="61c49-131">Bu denetleyicideki kod hakkında daha fazla bilgi için bkz. [Başlarken](tutorial-your-first-web-api.md) öğretici.</span><span class="sxs-lookup"><span data-stu-id="61c49-131">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="61c49-132">Yönlendirme bilgileri</span><span class="sxs-lookup"><span data-stu-id="61c49-132">Add Routing Information</span></span>

<span data-ttu-id="61c49-133">Ardından, URI yolu şekilde ekleyeceğiz, bir URI'leri formun &quot;/API'si/ürünler/&quot; denetleyiciye yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="61c49-133">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="61c49-134">İçinde **Çözüm Gezgini**, Global.asax Global.asax.cs arka plan kod dosyasını açmak için çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61c49-134">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="61c49-135">Aşağıdaki **kullanarak** deyimi.</span><span class="sxs-lookup"><span data-stu-id="61c49-135">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="61c49-136">Ardından aşağıdaki kodu ekleyin **uygulama\_Başlat** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="61c49-136">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="61c49-137">Yönlendirme tabloları hakkında daha fazla bilgi için bkz. [ASP.NET Web API'de yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="61c49-137">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="61c49-138">İstemci tarafı AJAX ekleme</span><span class="sxs-lookup"><span data-stu-id="61c49-138">Add Client-Side AJAX</span></span>

<span data-ttu-id="61c49-139">Tüm web istemcilerin erişebileceği bir API oluşturmak için gereken budur.</span><span class="sxs-lookup"><span data-stu-id="61c49-139">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="61c49-140">Şimdi, API'yi çağırmak için jQuery kullanan bir HTML sayfası ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="61c49-140">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="61c49-141">Ana sayfanıza emin olun (örneğin, *Site.Master*) içeren bir `ContentPlaceHolder` ile `ID="HeadContent"`:</span><span class="sxs-lookup"><span data-stu-id="61c49-141">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="61c49-142">Default.aspx dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="61c49-142">Open the file Default.aspx.</span></span> <span data-ttu-id="61c49-143">Ana içerik bölümü Demirbaş metni gösterildiği gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="61c49-143">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="61c49-144">Ardından, jQuery kaynak dosyasına bir başvuru ekleyin `HeaderContent` bölümü:</span><span class="sxs-lookup"><span data-stu-id="61c49-144">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="61c49-145">Not: Dosyadan sürükleyip bırakarak betik başvurusu kolayca ekleyebilirsiniz **Çözüm Gezgini** içine kod düzenleyicisi penceresi.</span><span class="sxs-lookup"><span data-stu-id="61c49-145">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="61c49-146">Aşağıdaki komut dosyası bloğu jQuery komut dosyası etiketi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="61c49-146">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="61c49-147">Belge yüklendiğinde bu betik bir AJAX isteğinde bulunur. &quot;API/ürünleri&quot;.</span><span class="sxs-lookup"><span data-stu-id="61c49-147">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="61c49-148">İstek, JSON biçiminde ürünlerin listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="61c49-148">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="61c49-149">Betik, ürün bilgisi HTML tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="61c49-149">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="61c49-150">Uygulamayı çalıştırdığınızda, şu şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="61c49-150">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
