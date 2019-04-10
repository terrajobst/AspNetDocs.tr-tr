---
uid: web-api/overview/older-versions/self-host-a-web-api
title: ASP.NET Web API 1 barındırma (C#)-ASP.NET 4.x
author: MikeWasson
description: Kod ile öğreticide, bir konsol uygulaması içinde bir web API'sini barındıran gösterilmektedir.
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7c73bf4734f8ed8a1bf93595c0847f611ad9cc15
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59409609"
---
# <a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="ede1f-103">Barındırılan ASP.NET Web API 1 (C#)</span><span class="sxs-lookup"><span data-stu-id="ede1f-103">Self-Host ASP.NET Web API 1 (C#)</span></span>

<span data-ttu-id="ede1f-104">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ede1f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="ede1f-105">Bu öğreticide, bir konsol uygulaması içinde bir web API'sini barındıran gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ede1f-105">This tutorial shows how to host a web API inside a console application.</span></span> <span data-ttu-id="ede1f-106">ASP.NET Web API, IIS gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="ede1f-106">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="ede1f-107">Web API'si kendi ana bilgisayar işlemi kendi kendine barındırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ede1f-107">You can self-host a web API in your own host process.</span></span> 
> 
> **<span data-ttu-id="ede1f-108">Yeni uygulama, barındırılan Web API'si için OWIN kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ede1f-108">New applications should use OWIN to self-host Web API.</span></span>** <span data-ttu-id="ede1f-109">Bkz: [OWIN, ASP.NET Web API 2 barındırma kullanmasını](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="ede1f-109">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ede1f-110">Bu öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="ede1f-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="ede1f-111">Web API 1</span><span class="sxs-lookup"><span data-stu-id="ede1f-111">Web API 1</span></span>
> - <span data-ttu-id="ede1f-112">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="ede1f-112">Visual Studio 2012</span></span>


## <a name="create-the-console-application-project"></a><span data-ttu-id="ede1f-113">Konsol uygulama projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ede1f-113">Create the Console Application Project</span></span>

<span data-ttu-id="ede1f-114">Visual Studio'yu başlatın ve seçin **yeni proje** gelen **Başlat** sayfası.</span><span class="sxs-lookup"><span data-stu-id="ede1f-114">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="ede1f-115">Veya **dosya** menüsünde **yeni** ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-115">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="ede1f-116">İçinde **şablonları** bölmesinde **yüklü şablonlar** genişletin **Visual C#** düğümü.</span><span class="sxs-lookup"><span data-stu-id="ede1f-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="ede1f-117">Altında **Visual C#** seçin **Windows**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-117">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="ede1f-118">Proje şablonları listesinde seçin **konsol uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-118">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="ede1f-119">Projeyi adlandırın &quot;SelfHost&quot; tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-119">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="ede1f-120">Hedef Framework'ü (Visual Studio 2010) ayarlama</span><span class="sxs-lookup"><span data-stu-id="ede1f-120">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="ede1f-121">Visual Studio 2010 kullanıyorsanız, hedef çerçeveyi .NET Framework 4.0 ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ede1f-121">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="ede1f-122">(Varsayılan olarak, proje şablonunun hedeflediği [.Net Framework istemci profili](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span><span class="sxs-lookup"><span data-stu-id="ede1f-122">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="ede1f-123">Çözüm Gezgini'nde projeye sağ tıklayıp seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-123">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="ede1f-124">İçinde **hedef Framework'ü** açılan listesinde, .NET Framework 4.0 için hedef Framework'ü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ede1f-124">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="ede1f-125">Değişikliği uygulamak için sorulduğunda **Evet**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-125">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="ede1f-126">NuGet Paket Yöneticisi'ni yükleyin</span><span class="sxs-lookup"><span data-stu-id="ede1f-126">Install NuGet Package Manager</span></span>

<span data-ttu-id="ede1f-127">NuGet Paket Yöneticisi, bir ASP.NET olmayan projeye Web API derlemeleri eklemek için en kolay yoludur.</span><span class="sxs-lookup"><span data-stu-id="ede1f-127">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="ede1f-128">NuGet Paket Yöneticisi'nin yüklü olup olmadığını denetlemek için **Araçları** Visual Studio'daki menü.</span><span class="sxs-lookup"><span data-stu-id="ede1f-128">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="ede1f-129">Bir menü öğesi adlı görürseniz **NuGet Paket Yöneticisi**, NuGet Paket Yöneticisi sahip.</span><span class="sxs-lookup"><span data-stu-id="ede1f-129">If you see a menu item called **NuGet Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="ede1f-130">NuGet Paket Yöneticisi'ni yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="ede1f-130">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="ede1f-131">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ede1f-131">Start Visual Studio.</span></span>
2. <span data-ttu-id="ede1f-132">Gelen **Araçları** menüsünde **Uzantılar ve güncelleştirmeler**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-132">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="ede1f-133">İçinde **Uzantılar ve güncelleştirmeler** iletişim kutusunda **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-133">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="ede1f-134">"Nuget Paket Yöneticisi", "NuGet Paket Yöneticisi" ifadesini görmüyorsanız arama kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="ede1f-134">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="ede1f-135">NuGet Paket Yöneticisi'ni seçip tıklayın **indirme**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-135">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="ede1f-136">İndirme tamamlandıktan sonra yüklemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="ede1f-136">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="ede1f-137">Yükleme tamamlandıktan sonra Visual Studio'yu yeniden başlatmanız istenebilir.</span><span class="sxs-lookup"><span data-stu-id="ede1f-137">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="ede1f-138">Web API NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="ede1f-138">Add the Web API NuGet Package</span></span>

<span data-ttu-id="ede1f-139">NuGet Paket Yöneticisi'ni yükledikten sonra Web API Self-Host paketini projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ede1f-139">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="ede1f-140">Gelen **Araçları** menüsünde **NuGet Paket Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-140">From the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="ede1f-141">*Not*: Bu menü öğesi, bu NuGet Paket Yöneticisi'nin yüklendiğinden emin olun görmüyorsanız.</span><span class="sxs-lookup"><span data-stu-id="ede1f-141">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="ede1f-142">Seçin **çözüm için NuGet paketlerini Yönet**</span><span class="sxs-lookup"><span data-stu-id="ede1f-142">Select **Manage NuGet Packages for Solution**</span></span>
3. <span data-ttu-id="ede1f-143">İçinde **NugGet paketlerini Yönet** iletişim kutusunda **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-143">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="ede1f-144">Arama kutusuna &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span><span class="sxs-lookup"><span data-stu-id="ede1f-144">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="ede1f-145">ASP.NET Web API Self konağı paketi seçin ve tıklayın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-145">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="ede1f-146">Paket yüklendikten sonra tıklayın **kapatmak** iletişim kutusunu kapatmak için.</span><span class="sxs-lookup"><span data-stu-id="ede1f-146">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="ede1f-147">Microsoft.AspNet.WebApi.SelfHost, değil AspNetWebApi.SelfHost adlı paketi yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ede1f-147">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="ede1f-148">Model ve denetleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="ede1f-148">Create the Model and Controller</span></span>

<span data-ttu-id="ede1f-149">Bu öğreticide aynı model ve denetleyici sınıflar olarak [Başlarken](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) öğretici.</span><span class="sxs-lookup"><span data-stu-id="ede1f-149">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="ede1f-150">Adlı bir ortak Sınıf Ekle `Product`.</span><span class="sxs-lookup"><span data-stu-id="ede1f-150">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="ede1f-151">Adlı bir ortak Sınıf Ekle `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="ede1f-151">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="ede1f-152">Bu sınıftan türetilen **System.Web.Http.ApiController**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-152">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="ede1f-153">Bu denetleyicideki kod hakkında daha fazla bilgi için bkz. [Başlarken](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) öğretici.</span><span class="sxs-lookup"><span data-stu-id="ede1f-153">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="ede1f-154">Bu denetleyici üç GET eylemleri tanımlar:</span><span class="sxs-lookup"><span data-stu-id="ede1f-154">This controller defines three GET actions:</span></span>

| <span data-ttu-id="ede1f-155">URI</span><span class="sxs-lookup"><span data-stu-id="ede1f-155">URI</span></span> | <span data-ttu-id="ede1f-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ede1f-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ede1f-157">/ api/ürünleri</span><span class="sxs-lookup"><span data-stu-id="ede1f-157">/api/products</span></span> | <span data-ttu-id="ede1f-158">Tüm ürünlerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="ede1f-158">Get a list of all products.</span></span> |
| <span data-ttu-id="ede1f-159">/API'si/ürünler/*kimliği*</span><span class="sxs-lookup"><span data-stu-id="ede1f-159">/api/products/*id*</span></span> | <span data-ttu-id="ede1f-160">Bir ürün kimliğine göre Al</span><span class="sxs-lookup"><span data-stu-id="ede1f-160">Get a product by ID.</span></span> |
| <span data-ttu-id="ede1f-161">/ API'si/ürünler /? kategori =*kategorisi*</span><span class="sxs-lookup"><span data-stu-id="ede1f-161">/api/products/?category=*category*</span></span> | <span data-ttu-id="ede1f-162">Kategoriye göre ürünlerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="ede1f-162">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="ede1f-163">Web API'si barındırın</span><span class="sxs-lookup"><span data-stu-id="ede1f-163">Host the Web API</span></span>

<span data-ttu-id="ede1f-164">Program.cs dosyasını açın ve aşağıdaki using deyimlerini:</span><span class="sxs-lookup"><span data-stu-id="ede1f-164">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="ede1f-165">Aşağıdaki kodu ekleyin **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ede1f-165">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="ede1f-166">(İsteğe bağlı) Bir HTTP URL'si Namespace ayırma ekleyin</span><span class="sxs-lookup"><span data-stu-id="ede1f-166">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="ede1f-167">Bu uygulamasının dinleyeceği `http://localhost:8080/`.</span><span class="sxs-lookup"><span data-stu-id="ede1f-167">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="ede1f-168">Varsayılan olarak, belirli bir HTTP adreste dinleme yönetici ayrıcalıkları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ede1f-168">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="ede1f-169">Bu nedenle öğreticiyi çalıştırdığınızda bu hatayı alabilirsiniz: "HTTP URL'si kaydedemedi http://+:8080/" Bu hatayı önlemek için iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="ede1f-169">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="ede1f-170">Visual Studio'yu yönetici izinleriyle çalıştırın veya</span><span class="sxs-lookup"><span data-stu-id="ede1f-170">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="ede1f-171">Netsh.exe URL ayırmak için hesap izinlerinize vermek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ede1f-171">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="ede1f-172">Netsh.exe kullanmak için yönetici ayrıcalıklarıyla bir komut istemi açın ve aşağıdaki komutu: aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="ede1f-172">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="ede1f-173">Burada *Makine\kullanıcı* kullanıcı hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="ede1f-173">where *machine\username* is your user account.</span></span>

<span data-ttu-id="ede1f-174">İşiniz bittiğinde kendi kendine barındırma, rezervasyon sildiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="ede1f-174">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="ede1f-175">Bir istemci uygulamasından (C#) Web API'si çağırma</span><span class="sxs-lookup"><span data-stu-id="ede1f-175">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="ede1f-176">Şimdi web API'si çağıran basit bir konsol uygulaması yazma.</span><span class="sxs-lookup"><span data-stu-id="ede1f-176">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="ede1f-177">Yeni bir konsol uygulaması projesi çözüme ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ede1f-177">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="ede1f-178">Çözüm Gezgini'nde çözüme sağ tıklayıp seçin **Yeni Proje Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-178">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="ede1f-179">Adlı yeni bir konsol uygulaması oluşturun &quot;ClientApp&quot;.</span><span class="sxs-lookup"><span data-stu-id="ede1f-179">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="ede1f-180">NuGet paketi ASP.NET Web API çekirdek kitaplıkları paketini eklemek için Yöneticisi'ni kullanın:</span><span class="sxs-lookup"><span data-stu-id="ede1f-180">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="ede1f-181">Araçlar menüsü'nden seçin **NuGet Paket Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-181">From the Tools menu, select **NuGet Package Manager**.</span></span>
- <span data-ttu-id="ede1f-182">Seçin **çözüm için NuGet paketlerini Yönet**</span><span class="sxs-lookup"><span data-stu-id="ede1f-182">Select **Manage NuGet Packages for Solution**</span></span>
- <span data-ttu-id="ede1f-183">İçinde **NuGet paketlerini Yönet** iletişim kutusunda **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-183">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="ede1f-184">Arama kutusuna &quot;System.NET.http.Formatting&quot;.</span><span class="sxs-lookup"><span data-stu-id="ede1f-184">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="ede1f-185">Microsoft ASP.NET Web API İstemci Kitaplığı paketi seçin ve tıklayın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-185">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="ede1f-186">Bir başvuru ClientApp SelfHost projeye ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ede1f-186">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="ede1f-187">Çözüm Gezgini'nde ClientApp projeye sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ede1f-187">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="ede1f-188">Seçin **Başvurusu Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-188">Select **Add Reference**.</span></span>
- <span data-ttu-id="ede1f-189">İçinde **başvuru Yöneticisi** iletişim altında **çözüm**seçin **projeleri**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-189">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="ede1f-190">SelfHost projeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="ede1f-190">Select the SelfHost project.</span></span>
- <span data-ttu-id="ede1f-191">**Tamam**'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ede1f-191">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="ede1f-192">Client/Program.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="ede1f-192">Open the Client/Program.cs file.</span></span> <span data-ttu-id="ede1f-193">Aşağıdaki **kullanarak** deyimi:</span><span class="sxs-lookup"><span data-stu-id="ede1f-193">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="ede1f-194">Statik bir ekleme **HttpClient** örneği:</span><span class="sxs-lookup"><span data-stu-id="ede1f-194">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="ede1f-195">Tüm ürünler, bir ürün Kimliğine göre listesi ve ürünleri listeler, kategoriye göre listelemek için aşağıdaki yöntemleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ede1f-195">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="ede1f-196">Bu yöntemlerin her biri aynı deseni izler:</span><span class="sxs-lookup"><span data-stu-id="ede1f-196">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="ede1f-197">Çağrı **HttpClient.GetAsync** uygun URI'ye bir GET isteği göndermek için.</span><span class="sxs-lookup"><span data-stu-id="ede1f-197">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="ede1f-198">Çağrı **HttpResponseMessage.EnsureSuccessStatusCode**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-198">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="ede1f-199">HTTP yanıtı durum bir hata kodu ise bu yöntem bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ede1f-199">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="ede1f-200">Çağrı **ReadAsAsync&lt;T&gt;**  HTTP yanıtı gelen bir CLR türü seri durumdan çıkarılacak.</span><span class="sxs-lookup"><span data-stu-id="ede1f-200">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="ede1f-201">Bu yöntem içinde tanımlanan bir genişletme yöntemi olduğunu **System.Net.Http.HttpContentExtensions**.</span><span class="sxs-lookup"><span data-stu-id="ede1f-201">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="ede1f-202">**GetAsync** ve **ReadAsAsync** hem de zaman uyumsuz yöntemler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="ede1f-202">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="ede1f-203">Döndürmeleri **görev** zaman uyumsuz işlemi temsil eden nesneleri.</span><span class="sxs-lookup"><span data-stu-id="ede1f-203">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="ede1f-204">Başlama **sonucu** özelliği işlem tamamlanana kadar iş parçacığını engeller.</span><span class="sxs-lookup"><span data-stu-id="ede1f-204">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="ede1f-205">HttpClient, engellemeyen çağrı yapmak nasıl dahil olmak üzere kullanma hakkında daha fazla bilgi için bkz. [bir Web API'si bir .NET istemcinin çağırma](../advanced/calling-a-web-api-from-a-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="ede1f-205">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="ede1f-206">Bu yöntemleri çağrılmadan önce BaseAddress özelliği için HttpClient örneği üzerinde ayarlanmış "`http://localhost:8080`".</span><span class="sxs-lookup"><span data-stu-id="ede1f-206">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="ede1f-207">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ede1f-207">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="ede1f-208">Bu aşağıdaki çıkışı oluşturmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ede1f-208">This should output the following.</span></span> <span data-ttu-id="ede1f-209">(İlk SelfHost uygulamayı çalıştırmak unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="ede1f-209">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
