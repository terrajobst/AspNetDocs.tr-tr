---
uid: web-api/overview/older-versions/self-host-a-web-api
title: Self-Host ASP.NET Web API 1 (C#)-ASP.NET 4. x
author: MikeWasson
description: Kod ile öğretici, bir Web API 'sinin bir konsol uygulaması içinde nasıl barındıralınacağını gösterir.
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525090"
---
# <a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="e16f6-103">Self-Host ASP.NET Web API 1 (C#)</span><span class="sxs-lookup"><span data-stu-id="e16f6-103">Self-Host ASP.NET Web API 1 (C#)</span></span>

<span data-ttu-id="e16f6-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e16f6-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="e16f6-105">Bu öğreticide, bir Web API 'sinin konsol uygulaması içinde nasıl barındırılacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e16f6-105">This tutorial shows how to host a web API inside a console application.</span></span> <span data-ttu-id="e16f6-106">ASP.NET Web API 'SI IIS gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="e16f6-106">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="e16f6-107">Kendi ana bilgisayar sürecinizdeki bir Web API 'sini kendi kendinize barındırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e16f6-107">You can self-host a web API in your own host process.</span></span> 
> 
> <span data-ttu-id="e16f6-108">**Yeni uygulamalar, Web API 'sini Self barındırmak için OWıN kullanmalıdır.**</span><span class="sxs-lookup"><span data-stu-id="e16f6-108">**New applications should use OWIN to self-host Web API.**</span></span> <span data-ttu-id="e16f6-109">Bkz. [OWIN kullanarak Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="e16f6-109">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e16f6-110">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="e16f6-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="e16f6-111">Web API 1</span><span class="sxs-lookup"><span data-stu-id="e16f6-111">Web API 1</span></span>
> - <span data-ttu-id="e16f6-112">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="e16f6-112">Visual Studio 2012</span></span>

## <a name="create-the-console-application-project"></a><span data-ttu-id="e16f6-113">Konsol uygulaması projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e16f6-113">Create the Console Application Project</span></span>

<span data-ttu-id="e16f6-114">Visual Studio 'Yu başlatın ve **Başlangıç** sayfasından **Yeni proje** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-114">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="e16f6-115">Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-115">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="e16f6-116">**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="e16f6-117">**Görsel C#** altında **Windows**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-117">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="e16f6-118">Proje şablonları listesinde **konsol uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-118">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="e16f6-119">Projeyi &quot;SelfHost&quot; olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-119">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="e16f6-120">Hedef Framework 'Ü ayarlama (Visual Studio 2010)</span><span class="sxs-lookup"><span data-stu-id="e16f6-120">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="e16f6-121">Visual Studio 2010 kullanıyorsanız, hedef çerçeveyi 4,0 .NET Framework değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-121">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="e16f6-122">(Varsayılan olarak, proje şablonu [.NET Framework Istemci profilini](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)hedefler.)</span><span class="sxs-lookup"><span data-stu-id="e16f6-122">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="e16f6-123">Çözüm Gezgini, projeye sağ tıklayın ve **Özellikler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-123">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="e16f6-124">**Hedef çerçeve** açılan listesinde, hedef framework 'ü .NET Framework 4,0 olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-124">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="e16f6-125">Değişikliği uygulamak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-125">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="e16f6-126">NuGet Paket Yöneticisi 'Ni yükler</span><span class="sxs-lookup"><span data-stu-id="e16f6-126">Install NuGet Package Manager</span></span>

<span data-ttu-id="e16f6-127">NuGet Paket Yöneticisi, Web API derlemelerini bir non-ASP.NET projesine eklemenin en kolay yoludur.</span><span class="sxs-lookup"><span data-stu-id="e16f6-127">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="e16f6-128">NuGet Paket Yöneticisi 'nin yüklü olup olmadığını denetlemek için Visual Studio 'daki **Araçlar** menüsüne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-128">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="e16f6-129">**NuGet Paket Yöneticisi**adlı bir menü öğesi görürseniz, NuGet Paket Yöneticisi ' ne sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="e16f6-129">If you see a menu item called **NuGet Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="e16f6-130">NuGet Paket Yöneticisi 'Ni yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="e16f6-130">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="e16f6-131">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-131">Start Visual Studio.</span></span>
2. <span data-ttu-id="e16f6-132">**Araçlar** menüsünde **Uzantılar ve güncelleştirmeler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-132">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="e16f6-133">**Uzantılar ve güncelleştirmeler** Iletişim kutusunda **çevrimiçi**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-133">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="e16f6-134">"NuGet Paket Yöneticisi" ni görmüyorsanız, arama kutusuna "NuGet Paket Yöneticisi" yazın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-134">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="e16f6-135">NuGet Paket Yöneticisi ' ni seçin ve **İndir**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-135">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="e16f6-136">Yükleme tamamlandıktan sonra yüklemesi istenir.</span><span class="sxs-lookup"><span data-stu-id="e16f6-136">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="e16f6-137">Yükleme tamamlandıktan sonra, Visual Studio 'Yu yeniden başlatmanız istenebilir.</span><span class="sxs-lookup"><span data-stu-id="e16f6-137">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="e16f6-138">Web API NuGet paketini ekleme</span><span class="sxs-lookup"><span data-stu-id="e16f6-138">Add the Web API NuGet Package</span></span>

<span data-ttu-id="e16f6-139">NuGet Paket Yöneticisi yüklendikten sonra, Web API Self-Host paketini projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-139">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="e16f6-140">**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-140">From the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="e16f6-141">*Not*: Bu menü öğesini görmüyorsanız, NuGet Paket Yöneticisi 'nin doğru şekilde yüklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e16f6-141">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="e16f6-142">**Çözüm Için NuGet Paketlerini Yönet** ' i seçin</span><span class="sxs-lookup"><span data-stu-id="e16f6-142">Select **Manage NuGet Packages for Solution**</span></span>
3. <span data-ttu-id="e16f6-143">**NugGet paketlerini Yönet** Iletişim kutusunda **çevrimiçi**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-143">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="e16f6-144">Arama kutusuna Microsoft. AspNet. WebApi. SelfHost&quot;&quot;yazın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-144">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="e16f6-145">ASP.NET Web API Self Host paketi ' ni seçin ve ardından **yükler**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-145">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="e16f6-146">Paket yüklendikten sonra, iletişim kutusunu kapatmak için **Kapat** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-146">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="e16f6-147">Microsoft. AspNet. WebApi. SelfHost adlı paketi, AspNetWebApi. SelfHost değil ' yi yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e16f6-147">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="e16f6-148">Modeli ve denetleyiciyi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e16f6-148">Create the Model and Controller</span></span>

<span data-ttu-id="e16f6-149">Bu [öğretici, başlangıç öğreticisiyle](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) aynı model ve denetleyici sınıflarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="e16f6-149">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="e16f6-150">`Product`adlı bir ortak sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-150">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="e16f6-151">`ProductsController`adlı bir ortak sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-151">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="e16f6-152">Bu sınıfı **System. Web. http. ApiController**öğesinden türet.</span><span class="sxs-lookup"><span data-stu-id="e16f6-152">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="e16f6-153">Bu denetleyicideki kod hakkında daha fazla bilgi için bkz. [Başlangıç](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="e16f6-153">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="e16f6-154">Bu denetleyici üç GET eylemini tanımlar:</span><span class="sxs-lookup"><span data-stu-id="e16f6-154">This controller defines three GET actions:</span></span>

| <span data-ttu-id="e16f6-155">URI</span><span class="sxs-lookup"><span data-stu-id="e16f6-155">URI</span></span> | <span data-ttu-id="e16f6-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e16f6-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e16f6-157">/api/Products</span><span class="sxs-lookup"><span data-stu-id="e16f6-157">/api/products</span></span> | <span data-ttu-id="e16f6-158">Tüm ürünlerin bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-158">Get a list of all products.</span></span> |
| <span data-ttu-id="e16f6-159">/api/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="e16f6-159">/api/products/*id*</span></span> | <span data-ttu-id="e16f6-160">KIMLIĞE göre bir ürün alın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-160">Get a product by ID.</span></span> |
| <span data-ttu-id="e16f6-161">/api/Products/? Category =*Kategori*</span><span class="sxs-lookup"><span data-stu-id="e16f6-161">/api/products/?category=*category*</span></span> | <span data-ttu-id="e16f6-162">Kategoriye göre ürünlerin bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-162">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="e16f6-163">Web API 'sini barındırma</span><span class="sxs-lookup"><span data-stu-id="e16f6-163">Host the Web API</span></span>

<span data-ttu-id="e16f6-164">Program.cs dosyasını açın ve aşağıdaki using deyimlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e16f6-164">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="e16f6-165">**Program** sınıfına aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-165">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="e16f6-166">Seçim HTTP URL ad alanı ayırması ekleme</span><span class="sxs-lookup"><span data-stu-id="e16f6-166">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="e16f6-167">Bu uygulama `http://localhost:8080/`dinler.</span><span class="sxs-lookup"><span data-stu-id="e16f6-167">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="e16f6-168">Varsayılan olarak, belirli bir HTTP adresini dinlemek için yönetici ayrıcalıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="e16f6-168">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="e16f6-169">Bu öğreticiyi çalıştırdığınızda şu hatayı alabilirsiniz: "HTTP URL 'SI kaydedilemedi http://+:8080/" Bu hatayı önlemenin iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="e16f6-169">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="e16f6-170">Visual Studio 'Yu yükseltilmiş yönetici izinleriyle çalıştırın veya</span><span class="sxs-lookup"><span data-stu-id="e16f6-170">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="e16f6-171">Hesap izinlerinize URL 'YI ayırmasını sağlamak için Netsh. exe ' yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-171">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="e16f6-172">Netsh. exe ' yi kullanmak için, yönetici ayrıcalıklarıyla bir komut istemi açın ve aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="e16f6-172">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="e16f6-173">burada, *MakineAdı* kullanıcı hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="e16f6-173">where *machine\username* is your user account.</span></span>

<span data-ttu-id="e16f6-174">Kendi kendine barındırmayı bitirdiğinizde ayırmayı silmeyi unutmayın:</span><span class="sxs-lookup"><span data-stu-id="e16f6-174">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="e16f6-175">Bir Istemci uygulamasından (C#) Web API 'sini çağırma</span><span class="sxs-lookup"><span data-stu-id="e16f6-175">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="e16f6-176">Web API 'sini çağıran basit bir konsol uygulaması yazalım.</span><span class="sxs-lookup"><span data-stu-id="e16f6-176">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="e16f6-177">Çözüme yeni bir konsol uygulama projesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e16f6-177">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="e16f6-178">Çözüm Gezgini, çözüme sağ tıklayın ve **Yeni Proje Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-178">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="e16f6-179">&quot;ClientApp&quot;adlı yeni bir konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e16f6-179">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="e16f6-180">ASP.NET Web API çekirdek kitaplıkları paketini eklemek için NuGet Paket Yöneticisi 'Ni kullanın:</span><span class="sxs-lookup"><span data-stu-id="e16f6-180">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="e16f6-181">Araçlar menüsünde **NuGet Paket Yöneticisi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-181">From the Tools menu, select **NuGet Package Manager**.</span></span>
- <span data-ttu-id="e16f6-182">**Çözüm Için NuGet Paketlerini Yönet** ' i seçin</span><span class="sxs-lookup"><span data-stu-id="e16f6-182">Select **Manage NuGet Packages for Solution**</span></span>
- <span data-ttu-id="e16f6-183">**NuGet Paketlerini Yönet** Iletişim kutusunda **çevrimiçi**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-183">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="e16f6-184">Arama kutusuna &quot;Microsoft. AspNet. WebApi. Client&quot;yazın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-184">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="e16f6-185">Microsoft ASP.NET Web API Istemci kitaplıkları paketini seçin ve ardından **Install**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-185">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="e16f6-186">ClientApp ' de SelfHost projesine bir başvuru ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e16f6-186">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="e16f6-187">Çözüm Gezgini, ClientApp projesine sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-187">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="e16f6-188">**Başvuru Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-188">Select **Add Reference**.</span></span>
- <span data-ttu-id="e16f6-189">**Başvuru Yöneticisi** iletişim kutusunda, **çözüm**altında **Projeler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-189">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="e16f6-190">SelfHost projesini seçin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-190">Select the SelfHost project.</span></span>
- <span data-ttu-id="e16f6-191">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-191">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="e16f6-192">Client/program. cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-192">Open the Client/Program.cs file.</span></span> <span data-ttu-id="e16f6-193">Aşağıdaki **using** ifadesini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e16f6-193">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="e16f6-194">Statik bir **HttpClient** örneği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e16f6-194">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="e16f6-195">Tüm ürünleri listelemek, KIMLIĞE göre ürün listelemek ve ürünleri kategoriye göre listelemek için aşağıdaki yöntemleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e16f6-195">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="e16f6-196">Bu yöntemlerin her biri aynı düzene uyar:</span><span class="sxs-lookup"><span data-stu-id="e16f6-196">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="e16f6-197">Uygun URI 'ye bir GET isteği göndermek için **HttpClient. GetAsync** çağrısı yapın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-197">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="e16f6-198">**HttpResponseMessage. EnsureSuccessStatusCode**öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-198">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="e16f6-199">HTTP yanıt durumu bir hata kodu ise, bu yöntem bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e16f6-199">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="e16f6-200">HTTP yanıtından bir CLR türü serisini kaldırmak için **Readasasync&lt;t&gt;** çağırın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-200">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="e16f6-201">Bu yöntem, **System .net. http. Httpcontenbir**'da tanımlanan bir genişletme yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="e16f6-201">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="e16f6-202">**GetAsync** ve **readasasync** yöntemlerinin her ikisi de zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="e16f6-202">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="e16f6-203">Zaman uyumsuz işlemi temsil eden **görev** nesnelerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="e16f6-203">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="e16f6-204">**Result** özelliğinin alınması, işlem tamamlanana kadar iş parçacığını engeller.</span><span class="sxs-lookup"><span data-stu-id="e16f6-204">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="e16f6-205">Engelleme olmayan çağrılar yapma da dahil olmak üzere HttpClient kullanımı hakkında daha fazla bilgi için bkz. [.net Istemcisinden Web API çağırma](../advanced/calling-a-web-api-from-a-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="e16f6-205">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="e16f6-206">Bu yöntemleri çağırmadan önce HttpClient örneğindeki BaseAddress özelliğini "`http://localhost:8080`" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e16f6-206">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="e16f6-207">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e16f6-207">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="e16f6-208">Bu, aşağıdaki çıktıyı göstermelidir.</span><span class="sxs-lookup"><span data-stu-id="e16f6-208">This should output the following.</span></span> <span data-ttu-id="e16f6-209">(Önce SelfHost uygulamasını çalıştırmayı unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="e16f6-209">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
