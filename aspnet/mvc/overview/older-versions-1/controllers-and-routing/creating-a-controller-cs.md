---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: Denetleyici oluşturma (C#) | Microsoft Docs
author: StephenWalther
description: Bu öğreticide, Stephen Walther bir ASP.NET MVC uygulamasına nasıl denetleyici ekleyebileceğiniz gösterilmektedir.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: 6e3d0bae7f07410637c2b06c500d94a02c821f5c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544081"
---
# <a name="creating-a-controller-c"></a><span data-ttu-id="6b99e-103">Denetleyici Oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="6b99e-103">Creating a Controller (C#)</span></span>

<span data-ttu-id="6b99e-104">ile [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="6b99e-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="6b99e-105">Bu öğreticide, Stephen Walther bir ASP.NET MVC uygulamasına nasıl denetleyici ekleyebileceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6b99e-105">In this tutorial, Stephen Walther demonstrates how you can add a controller to an ASP.NET MVC application.</span></span>

<span data-ttu-id="6b99e-106">Bu öğreticinin amacı, yeni ASP.NET MVC denetleyicilerini nasıl oluşturabileceğiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6b99e-106">The goal of this tutorial is to explain how you can create new ASP.NET MVC controllers.</span></span> <span data-ttu-id="6b99e-107">Visual Studio denetleyici Ekle menü seçeneğini kullanarak ve el ile bir sınıf dosyası oluşturarak denetleyiciler oluşturmayı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6b99e-107">You learn how to create controllers both by using the Visual Studio Add Controller menu option and by creating a class file by hand.</span></span>

### <a name="using-the-add-controller-menu-option"></a><span data-ttu-id="6b99e-108">Denetleyici Ekle menü seçeneğini kullanma</span><span class="sxs-lookup"><span data-stu-id="6b99e-108">Using the Add Controller Menu Option</span></span>

<span data-ttu-id="6b99e-109">Yeni bir denetleyici oluşturmanın en kolay yolu, Visual Studio Çözüm Gezgini penceresinde Controllers klasörüne sağ tıklayıp **Ekle, denetleyici** menü seçeneğini (bkz. Şekil 1) seçer.</span><span class="sxs-lookup"><span data-stu-id="6b99e-109">The easiest way to create a new controller is to right-click the Controllers folder in the Visual Studio Solution Explorer window and select the **Add, Controller** menu option (see Figure 1).</span></span> <span data-ttu-id="6b99e-110">Bu menü seçeneği belirlendiğinde, **Denetleyici Ekle** iletişim kutusu açılır (bkz. Şekil 2).</span><span class="sxs-lookup"><span data-stu-id="6b99e-110">Selecting this menu option opens the **Add Controller** dialog (see Figure 2).</span></span>

<span data-ttu-id="6b99e-111">[Yeni proje iletişim kutusunu ![](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6b99e-111">[![The New Project dialog box](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)</span></span>

<span data-ttu-id="6b99e-112">**Şekil 01**: yeni bir denetleyici ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-controller-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="6b99e-112">**Figure 01**: Adding a new controller([Click to view full-size image](creating-a-controller-cs/_static/image2.png))</span></span>

<span data-ttu-id="6b99e-113">[Yeni proje iletişim kutusunu ![](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="6b99e-113">[![The New Project dialog box](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)</span></span>

<span data-ttu-id="6b99e-114">**Şekil 02**: denetleyici Ekle iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-controller-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="6b99e-114">**Figure 02**: The Add Controller dialog ([Click to view full-size image](creating-a-controller-cs/_static/image4.png))</span></span>

<span data-ttu-id="6b99e-115">Denetleyici adının ilk bölümünün **Denetleyici Ekle** iletişim kutusunda vurgulandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6b99e-115">Notice that the first part of the controller name is highlighted in the **Add Controller** dialog.</span></span> <span data-ttu-id="6b99e-116">Her denetleyici adının son ek *denetleyicisiyle*bitmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b99e-116">Every controller name must end with the suffix *Controller*.</span></span> <span data-ttu-id="6b99e-117">Örneğin, *ProductController* adlı bir denetleyici oluşturabilirsiniz, ancak *ürün*adında bir denetleyici oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="6b99e-117">For example, you can create a controller named *ProductController* but not a controller named *Product*.</span></span>

<span data-ttu-id="6b99e-118">*Denetleyici* son eki eksik olan bir denetleyici oluşturursanız, denetleyiciyi çağıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="6b99e-118">If you create a controller that is missing the *Controller* suffix then you won't be able to invoke the controller.</span></span> <span data-ttu-id="6b99e-119">Bunu yapma-bu hata yapıldıktan sonra hayata daha az saat harcandım.</span><span class="sxs-lookup"><span data-stu-id="6b99e-119">Don't do this -- I've wasted countless hours of my life after making this mistake.</span></span>

<span data-ttu-id="6b99e-120">**Listeleme 1-Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="6b99e-120">**Listing 1 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

<span data-ttu-id="6b99e-121">Denetleyiciler klasöründe her zaman denetleyici oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b99e-121">You should always create controllers in the Controllers folder.</span></span> <span data-ttu-id="6b99e-122">Aksi takdirde, ASP.NET MVC 'nin kurallarını ihlal edersiniz ve diğer geliştiriciler uygulamanızı daha zor bir zamana göre anlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="6b99e-122">Otherwise, you'll be violating the conventions of ASP.NET MVC and other developers will have a more difficult time understanding your application.</span></span>

### <a name="scaffolding-action-methods"></a><span data-ttu-id="6b99e-123">Yapı iskelesi eylem yöntemleri</span><span class="sxs-lookup"><span data-stu-id="6b99e-123">Scaffolding Action Methods</span></span>

<span data-ttu-id="6b99e-124">Bir denetleyici oluşturduğunuzda, otomatik olarak Create, Update ve details eylem yöntemleri oluşturma seçeneğiniz vardır (bkz. Şekil 3).</span><span class="sxs-lookup"><span data-stu-id="6b99e-124">When you create a controller, you have the option to generate Create, Update, and Details action methods automatically (see Figure 3).</span></span> <span data-ttu-id="6b99e-125">Bu seçeneği belirlerseniz, liste 2 ' deki denetleyici sınıfı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6b99e-125">If you select this option then the controller class in Listing 2 is generated.</span></span>

<span data-ttu-id="6b99e-126">[eylem yöntemlerini otomatik olarak oluşturma ![](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="6b99e-126">[![Creating action methods automatically](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)</span></span>

<span data-ttu-id="6b99e-127">**Şekil 03**: otomatik olarak eylem yöntemleri oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-controller-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="6b99e-127">**Figure 03**: Creating action methods automatically ([Click to view full-size image](creating-a-controller-cs/_static/image6.png))</span></span>

<span data-ttu-id="6b99e-128">**Listeleme 2-Controllers\CustomerController.cs**</span><span class="sxs-lookup"><span data-stu-id="6b99e-128">**Listing 2 - Controllers\CustomerController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

<span data-ttu-id="6b99e-129">Bu oluşturulan Yöntemler saplama yöntemleridir.</span><span class="sxs-lookup"><span data-stu-id="6b99e-129">These generated methods are stub methods.</span></span> <span data-ttu-id="6b99e-130">Müşterinin ayrıntılarını oluşturmak, güncelleştirmek ve göstermek için gerçek mantığı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b99e-130">You must add the actual logic for creating, updating, and showing details for a customer yourself.</span></span> <span data-ttu-id="6b99e-131">Ancak, saplama yöntemleri size iyi bir başlangıç noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b99e-131">But, the stub methods provide you with a nice starting point.</span></span>

### <a name="creating-a-controller-class"></a><span data-ttu-id="6b99e-132">Denetleyici sınıfı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b99e-132">Creating a Controller Class</span></span>

<span data-ttu-id="6b99e-133">ASP.NET MVC denetleyicisi yalnızca bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="6b99e-133">The ASP.NET MVC controller is just a class.</span></span> <span data-ttu-id="6b99e-134">İsterseniz, uygun bir Visual Studio denetleyicisi yapı iskelesi yoksayabilirsiniz ve el ile bir denetleyici sınıfı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b99e-134">If you prefer, you can ignore the convenient Visual Studio controller scaffolding and create a controller class by hand.</span></span> <span data-ttu-id="6b99e-135">Aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="6b99e-135">Follow these steps:</span></span>

1. <span data-ttu-id="6b99e-136">Denetleyiciler klasörüne sağ tıklayın ve **Ekle, yeni öğe** menü seçeneğini belirleyin ve **sınıf** şablonunu seçin (bkz. Şekil 4).</span><span class="sxs-lookup"><span data-stu-id="6b99e-136">Right-click the Controllers folder and select the menu option **Add, New Item** and select the **Class** template (see Figure 4).</span></span>
2. <span data-ttu-id="6b99e-137">Yeni sınıfı PersonController.cs olarak adlandırın ve **Ekle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b99e-137">Name the new class PersonController.cs and click the **Add** button.</span></span>
3. <span data-ttu-id="6b99e-138">Elde edilen sınıf dosyasını, sınıfın temel System. Web. Mvc. Controller sınıfından devrayor şekilde değiştirin (bkz. Listeleme 3).</span><span class="sxs-lookup"><span data-stu-id="6b99e-138">Modify the resulting class file so that the class inherits from the base System.Web.Mvc.Controller class (see Listing 3).</span></span>

<span data-ttu-id="6b99e-139">[Yeni bir sınıf oluşturma ![](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="6b99e-139">[![Creating a new class](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)</span></span>

<span data-ttu-id="6b99e-140">**Şekil 04**: yeni bir sınıf oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-controller-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="6b99e-140">**Figure 04**: Creating a new class([Click to view full-size image](creating-a-controller-cs/_static/image8.png))</span></span>

<span data-ttu-id="6b99e-141">**Listeleme 3-Controllers\PersonController.cs**</span><span class="sxs-lookup"><span data-stu-id="6b99e-141">**Listing 3 - Controllers\PersonController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

<span data-ttu-id="6b99e-142">Listeleme 3 ' teki denetleyici, "Merhaba Dünya!" dizesini döndüren Index () adlı bir eylem gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b99e-142">The controller in Listing 3 exposes one action named Index() that returns the string "Hello World!".</span></span> <span data-ttu-id="6b99e-143">Uygulamanızı çalıştırarak ve aşağıdakine benzer bir URL isteğinde bulunarak bu denetleyici eylemini çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6b99e-143">You can invoke this controller action by running your application and requesting a URL like the following:</span></span>

`http://localhost:40071/Person`

> [!NOTE]
> 
> <span data-ttu-id="6b99e-144">ASP.NET geliştirme sunucusu rastgele bir bağlantı noktası numarası kullanır (örneğin, 40071).</span><span class="sxs-lookup"><span data-stu-id="6b99e-144">The ASP.NET Development Server uses a random port number (for example, 40071).</span></span> <span data-ttu-id="6b99e-145">Denetleyiciyi çağırmak için bir URL girerken, doğru bağlantı noktası numarasını sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b99e-145">When entering a URL to invoke a controller, you'll need to supply the right port number.</span></span> <span data-ttu-id="6b99e-146">Farenizi Windows bildirim alanındaki (ekranınızın sağ alt tarafındaki) ASP.NET geliştirme sunucusu simgesinin üzerine getirerek bağlantı noktası numarasını belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b99e-146">You can determine the port number by hovering your mouse over the icon for the ASP.NET Development Server in the Windows Notification Area (bottom-right of your screen).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="6b99e-147">[Önceki](adding-dynamic-content-to-a-cached-page-cs.md)
> [İleri](creating-an-action-cs.md)</span><span class="sxs-lookup"><span data-stu-id="6b99e-147">[Previous](adding-dynamic-content-to-a-cached-page-cs.md)
[Next](creating-an-action-cs.md)</span></span>
