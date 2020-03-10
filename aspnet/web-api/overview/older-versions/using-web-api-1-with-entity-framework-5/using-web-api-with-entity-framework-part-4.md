---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: '4\. Bölüm: yönetici görünümü ekleme | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556016"
---
# <a name="part-4-adding-an-admin-view"></a><span data-ttu-id="31b2a-102">4\. Bölüm: yönetici görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="31b2a-102">Part 4: Adding an Admin View</span></span>

<span data-ttu-id="31b2a-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="31b2a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="31b2a-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="31b2a-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a><span data-ttu-id="31b2a-105">Yönetici görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="31b2a-105">Add an Admin View</span></span>

<span data-ttu-id="31b2a-106">Şimdi istemci tarafına ve yönetici denetleyicisinden veri kullanabilen bir sayfa ekleyecek.</span><span class="sxs-lookup"><span data-stu-id="31b2a-106">Now we'll turn to the client side, and add a page that can consume data from the Admin controller.</span></span> <span data-ttu-id="31b2a-107">Bu sayfa, kullanıcıların denetleyiciye AJAX istekleri göndererek ürün oluşturmalarına, düzenlemesine veya silmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="31b2a-107">The page will allow users to create, edit, or delete products, by sending AJAX requests to the controller.</span></span>

<span data-ttu-id="31b2a-108">Çözüm Gezgini, denetleyiciler klasörünü genişletin ve HomeController.cs adlı dosyayı açın.</span><span class="sxs-lookup"><span data-stu-id="31b2a-108">In Solution Explorer, expand the Controllers folder and open the file named HomeController.cs.</span></span> <span data-ttu-id="31b2a-109">Bu dosya bir MVC denetleyicisi içeriyor.</span><span class="sxs-lookup"><span data-stu-id="31b2a-109">This file contains an MVC controller.</span></span> <span data-ttu-id="31b2a-110">`Admin`adlı bir yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="31b2a-110">Add a method named `Admin`:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

<span data-ttu-id="31b2a-111">**Httprouteurl** yöntemi, Web API 'sine URI 'yi oluşturur ve bunu daha sonra Görünüm çantasında depoluyoruz.</span><span class="sxs-lookup"><span data-stu-id="31b2a-111">The **HttpRouteUrl** method creates the URI to the web API, and we store this in the view bag for later.</span></span>

<span data-ttu-id="31b2a-112">Sonra, metin imlecini `Admin` Action yönteminin içinde konumlandırın, sonra sağ tıklayıp **Görünüm Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="31b2a-112">Next, position the text cursor within the `Admin` action method, then right-click and select **Add View**.</span></span> <span data-ttu-id="31b2a-113">Bu işlem, **Görünüm Ekle** iletişim kutusunu getirir.</span><span class="sxs-lookup"><span data-stu-id="31b2a-113">This will bring up the **Add View** dialog.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

<span data-ttu-id="31b2a-114">**Görünüm Ekle** iletişim kutusunda "Yönetici" görünümünü adlandırın.</span><span class="sxs-lookup"><span data-stu-id="31b2a-114">In the **Add View** dialog, name the view "Admin".</span></span> <span data-ttu-id="31b2a-115">**Kesin olarak belirlenmiş görünüm oluştur**etiketli onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="31b2a-115">Select the check box labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="31b2a-116">**Model sınıfı**altında "Product (productstore. modeller)" öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="31b2a-116">Under **Model Class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="31b2a-117">Diğer tüm seçenekleri varsayılan değerler olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="31b2a-117">Leave all the other options as their default values.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

<span data-ttu-id="31b2a-118">**Ekle** ' ye tıklamak, görünümler/giriş bölümünde admin. cshtml adlı bir dosya ekler.</span><span class="sxs-lookup"><span data-stu-id="31b2a-118">Clicking **Add** adds a file named Admin.cshtml under Views/Home.</span></span> <span data-ttu-id="31b2a-119">Bu dosyayı açın ve aşağıdaki HTML 'yi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="31b2a-119">Open this file and add the following HTML.</span></span> <span data-ttu-id="31b2a-120">Bu HTML sayfanın yapısını tanımlar, ancak henüz hiçbir işlev kablolu değildir.</span><span class="sxs-lookup"><span data-stu-id="31b2a-120">This HTML defines the structure of the page, but no functionality is wired up yet.</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a><span data-ttu-id="31b2a-121">Yönetici sayfasına bağlantı oluştur</span><span class="sxs-lookup"><span data-stu-id="31b2a-121">Create a Link to the Admin Page</span></span>

<span data-ttu-id="31b2a-122">Çözüm Gezgini, görünümler klasörünü genişletin ve ardından paylaşılan klasörü genişletin.</span><span class="sxs-lookup"><span data-stu-id="31b2a-122">In Solution Explorer, expand the Views folder and then expand the Shared folder.</span></span> <span data-ttu-id="31b2a-123">\_Layout. cshtml adlı dosyayı açın.</span><span class="sxs-lookup"><span data-stu-id="31b2a-123">Open the file named \_Layout.cshtml.</span></span> <span data-ttu-id="31b2a-124">ID = "Menu" olan **ul** öğesini ve yönetici görünümü için bir eylem bağlantısını bulun:</span><span class="sxs-lookup"><span data-stu-id="31b2a-124">Locate the **ul** element with id = "menu", and an action link for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> <span data-ttu-id="31b2a-125">Örnek projede, "logonuzu buraya" yazmanız gibi birkaç başka yüzeysel değişikliği yaptık.</span><span class="sxs-lookup"><span data-stu-id="31b2a-125">In the sample project, I made a few other cosmetic changes, such as replacing the string "Your logo here".</span></span> <span data-ttu-id="31b2a-126">Bunlar, uygulamanın işlevselliğini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="31b2a-126">These don't affect the functionality of the application.</span></span> <span data-ttu-id="31b2a-127">Projeyi indirebilir ve dosyaları karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31b2a-127">You can download the project and compare the files.</span></span>

<span data-ttu-id="31b2a-128">Uygulamayı çalıştırın ve giriş sayfasının en üstünde görünen "Yönetici" bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="31b2a-128">Run the application and click the "Admin" link that appears at the top of the home page.</span></span> <span data-ttu-id="31b2a-129">Yönetici sayfası aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="31b2a-129">The Admin page should look like the following:</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

<span data-ttu-id="31b2a-130">Şu anda sayfa hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="31b2a-130">Right now, the page doesn't do anything.</span></span> <span data-ttu-id="31b2a-131">Bir sonraki bölümde, dinamik bir kullanıcı arabirimi oluşturmak için altını gizleme. js ' yi kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="31b2a-131">In the next section, we'll use Knockout.js to create a dynamic UI.</span></span>

## <a name="add-authorization"></a><span data-ttu-id="31b2a-132">Yetkilendirme Ekle</span><span class="sxs-lookup"><span data-stu-id="31b2a-132">Add Authorization</span></span>

<span data-ttu-id="31b2a-133">Yönetici sayfasına şu anda siteyi ziyaret eden herkes erişebilir.</span><span class="sxs-lookup"><span data-stu-id="31b2a-133">The Admin page is currently accessible to anyone visiting the site.</span></span> <span data-ttu-id="31b2a-134">Bunu, yöneticilere izinleri kısıtlamak için değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="31b2a-134">Let's change this to restrict permission to administrators.</span></span>

<span data-ttu-id="31b2a-135">Bir "Yönetici" rolü ve bir yönetici kullanıcı ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="31b2a-135">Start by adding an "Administrator" role and an administrator user.</span></span> <span data-ttu-id="31b2a-136">Çözüm Gezgini, filtreler klasörünü genişletin ve InitializeSimpleMembershipAttribute.cs adlı dosyayı açın.</span><span class="sxs-lookup"><span data-stu-id="31b2a-136">In Solution Explorer, expand the Filters folder and open the file named InitializeSimpleMembershipAttribute.cs.</span></span> <span data-ttu-id="31b2a-137">`SimpleMembershipInitializer` oluşturucusunu bulun.</span><span class="sxs-lookup"><span data-stu-id="31b2a-137">Locate the `SimpleMembershipInitializer` constructor.</span></span> <span data-ttu-id="31b2a-138">**WebSecurity. InitializeDatabaseConnection**çağrısından sonra aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="31b2a-138">After the call to **WebSecurity.InitializeDatabaseConnection**, add the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

<span data-ttu-id="31b2a-139">Bu, "Yönetici" rolünü eklemenin ve rol için bir kullanıcı oluşturmanın hızlı ve kirli bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="31b2a-139">This is a quick-and-dirty way to add the "Administrator" role and create a user for the role.</span></span>

<span data-ttu-id="31b2a-140">Çözüm Gezgini, denetleyiciler klasörünü genişletin ve HomeController.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="31b2a-140">In Solution Explorer, expand the Controllers folder and open the HomeController.cs file.</span></span> <span data-ttu-id="31b2a-141">`Admin` metoduna **Yetkilendir** özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="31b2a-141">Add the **Authorize** attribute to the `Admin` method.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

<span data-ttu-id="31b2a-142">AdminController.cs dosyasını açın ve tüm `AdminController` sınıfına **Yetkilendir** özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="31b2a-142">Open the AdminController.cs file and add the **Authorize** attribute to the entire `AdminController` class.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="31b2a-143">MVC ve Web API 'SI, farklı ad alanlarında **Yetkilendirme** özniteliklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="31b2a-143">MVC and Web API both define **Authorize** attributes, in different namespaces.</span></span> <span data-ttu-id="31b2a-144">MVC, **System. Web. Mvc. AuthorizeAttribute**kullanır, Web API 'si **System. Web. http. AuthorizeAttribute**kullanır.</span><span class="sxs-lookup"><span data-stu-id="31b2a-144">MVC uses **System.Web.Mvc.AuthorizeAttribute**, while Web API uses **System.Web.Http.AuthorizeAttribute**.</span></span>

<span data-ttu-id="31b2a-145">Artık yönetici sayfasını yalnızca yöneticiler görüntüleyebilir.</span><span class="sxs-lookup"><span data-stu-id="31b2a-145">Now only administrators can view the Admin page.</span></span> <span data-ttu-id="31b2a-146">Ayrıca, yönetici denetleyicisine bir HTTP isteği gönderirseniz, istek bir kimlik doğrulama tanımlama bilgisi içermelidir.</span><span class="sxs-lookup"><span data-stu-id="31b2a-146">Also, if you send an HTTP request to the Admin controller, the request must contain an authentication cookie.</span></span> <span data-ttu-id="31b2a-147">Aksi takdirde, sunucu bir HTTP 401 (yetkisiz) yanıtı gönderir.</span><span class="sxs-lookup"><span data-stu-id="31b2a-147">If not, the server sends an HTTP 401 (Unauthorized) response.</span></span> <span data-ttu-id="31b2a-148">Bunu, `http://localhost:*port*/api/admin`için bir GET isteği göndererek Fiddler 'da görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31b2a-148">You can see this in Fiddler by sending a GET request to `http://localhost:*port*/api/admin`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="31b2a-149">[Önceki](using-web-api-with-entity-framework-part-3.md)
> [İleri](using-web-api-with-entity-framework-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="31b2a-149">[Previous](using-web-api-with-entity-framework-part-3.md)
[Next](using-web-api-with-entity-framework-part-5.md)</span></span>
