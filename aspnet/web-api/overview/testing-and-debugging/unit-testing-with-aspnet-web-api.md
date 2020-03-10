---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: Birim testi ASP.NET Web API 2 | Microsoft Docs
author: Rick-Anderson
description: Bu kılavuz ve uygulama, Web API 2 uygulamanız için basit birim testlerin nasıl oluşturulacağını göstermektedir. Bu öğreticide bir birim testi proj 'i nasıl dahil edileceğini gösterilmektedir...
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554973"
---
# <a name="unit-testing-aspnet-web-api-2"></a><span data-ttu-id="a3bd3-104">Birim testi ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="a3bd3-104">Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="a3bd3-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="a3bd3-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="a3bd3-106">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="a3bd3-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="a3bd3-107">Bu kılavuz ve uygulama, Web API 2 uygulamanız için basit birim testlerin nasıl oluşturulacağını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-107">This guidance and application demonstrate how to create simple unit tests for your Web API 2 application.</span></span> <span data-ttu-id="a3bd3-108">Bu öğreticide, çözümünüze bir birim testi projesinin nasıl dahil edileceğini ve döndürülen değerleri bir denetleyici yönteminden denetleyen test yöntemlerini nasıl yazacağınız gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-108">This tutorial shows how to include a unit test project in your solution, and write test methods that check the returned values from a controller method.</span></span>
>
> <span data-ttu-id="a3bd3-109">Bu öğreticide, ASP.NET Web API 'sinin temel kavramları hakkında bilgi sahibi olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-109">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="a3bd3-110">Tanıtım öğreticisi için bkz. [ASP.NET Web API 2 Ile çalışmaya](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)başlama.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-110">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> <span data-ttu-id="a3bd3-111">Bu konudaki birim testleri, basit veri senaryolarıyla kasıtlı olarak sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-111">The unit tests in this topic are intentionally limited to simple data scenarios.</span></span> <span data-ttu-id="a3bd3-112">Birim testi daha gelişmiş veri senaryoları için bkz. [ASP.NET Web API 2 birim testi sırasında Mocking Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="a3bd3-112">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a3bd3-113">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="a3bd3-113">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="a3bd3-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a3bd3-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="a3bd3-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="a3bd3-115">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="a3bd3-116">Bu konuda</span><span class="sxs-lookup"><span data-stu-id="a3bd3-116">In this topic</span></span>

<span data-ttu-id="a3bd3-117">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="a3bd3-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="a3bd3-118">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a3bd3-118">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="a3bd3-119">Kodu indir</span><span class="sxs-lookup"><span data-stu-id="a3bd3-119">Download code</span></span>](#download)
- [<span data-ttu-id="a3bd3-120">Birim testi projesiyle uygulama oluştur</span><span class="sxs-lookup"><span data-stu-id="a3bd3-120">Create application with unit test project</span></span>](#appwithunittest)
    - [<span data-ttu-id="a3bd3-121">Uygulamayı oluştururken birim testi projesi Ekle</span><span class="sxs-lookup"><span data-stu-id="a3bd3-121">Add unit test project when creating the application</span></span>](#whencreate)
    - [<span data-ttu-id="a3bd3-122">Varolan bir uygulamaya birim testi projesi Ekle</span><span class="sxs-lookup"><span data-stu-id="a3bd3-122">Add unit test project to an existing application</span></span>](#addtoexisting)
- [<span data-ttu-id="a3bd3-123">Web API 2 uygulamasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="a3bd3-123">Set up the Web API 2 application</span></span>](#setupproject)
- [<span data-ttu-id="a3bd3-124">NuGet paketlerini test projesine yükler</span><span class="sxs-lookup"><span data-stu-id="a3bd3-124">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="a3bd3-125">Test oluştur</span><span class="sxs-lookup"><span data-stu-id="a3bd3-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="a3bd3-126">Testleri Çalıştır</span><span class="sxs-lookup"><span data-stu-id="a3bd3-126">Run tests</span></span>](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="a3bd3-127">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a3bd3-127">Prerequisites</span></span>

<span data-ttu-id="a3bd3-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional veya Enterprise sürümü</span><span class="sxs-lookup"><span data-stu-id="a3bd3-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="a3bd3-129">Kodu indirin</span><span class="sxs-lookup"><span data-stu-id="a3bd3-129">Download code</span></span>

<span data-ttu-id="a3bd3-130">[Tamamlanmış projeyi](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)indirin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-130">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="a3bd3-131">İndirilebilir proje, bu konu için birim test kodu ve [birim testi ASP.NET Web API konusu olduğunda Mocking Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) içerir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-131">The downloadable project includes unit test code for this topic and for the [Mocking Entity Framework when Unit Testing ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="a3bd3-132">Birim testi projesiyle uygulama oluştur</span><span class="sxs-lookup"><span data-stu-id="a3bd3-132">Create application with unit test project</span></span>

<span data-ttu-id="a3bd3-133">Uygulamanızı oluştururken bir birim testi projesi oluşturabilir veya var olan bir uygulamaya bir birim testi projesi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-133">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="a3bd3-134">Bu öğreticide, birim testi projesi oluşturmak için her iki yöntem de gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-134">This tutorial shows both methods for creating a unit test project.</span></span> <span data-ttu-id="a3bd3-135">Bu öğreticiyi izlemek için her iki yaklaşımı de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-135">To follow this tutorial, you can use either approach.</span></span>

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a><span data-ttu-id="a3bd3-136">Uygulamayı oluştururken birim testi projesi Ekle</span><span class="sxs-lookup"><span data-stu-id="a3bd3-136">Add unit test project when creating the application</span></span>

<span data-ttu-id="a3bd3-137">**Storeapp**adlı yeni bir ASP.NET Web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-137">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

![proje oluştur](unit-testing-with-aspnet-web-api/_static/image1.png)

<span data-ttu-id="a3bd3-139">Yeni ASP.NET proje penceresinde **boş** şablonu seçin ve Web API 'si için klasörler ve çekirdek başvurular ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-139">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="a3bd3-140">**Birim testleri Ekle** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-140">Select the **Add unit tests** option.</span></span> <span data-ttu-id="a3bd3-141">Birim testi projesi, otomatik olarak **Storeapp. Tests**olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-141">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="a3bd3-142">Bu adı koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-142">You can keep this name.</span></span>

![birim testi projesi oluştur](unit-testing-with-aspnet-web-api/_static/image2.png)

<span data-ttu-id="a3bd3-144">Uygulamayı oluşturduktan sonra, bunu iki proje içerdiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-144">After creating the application, you will see it contains two projects.</span></span>

![iki proje](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a><span data-ttu-id="a3bd3-146">Varolan bir uygulamaya birim testi projesi Ekle</span><span class="sxs-lookup"><span data-stu-id="a3bd3-146">Add unit test project to an existing application</span></span>

<span data-ttu-id="a3bd3-147">Uygulamanızı oluştururken birim testi projesi oluşturmadıysanız, herhangi bir zamanda bir tane ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-147">If you did not create the unit test project when you created your application, you can add one at any time.</span></span> <span data-ttu-id="a3bd3-148">Örneğin, StoreApp adlı bir uygulamanız olduğunu ve birim testleri eklemek istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-148">For example, suppose you already have an application named StoreApp, and you want to add unit tests.</span></span> <span data-ttu-id="a3bd3-149">Bir birim testi projesi eklemek için çözümünüze sağ tıklayın ve **Ekle** ve **Yeni proje**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-149">To add a unit test project, right-click your solution and select **Add** and **New Project**.</span></span>

![çözüme yeni proje Ekle](unit-testing-with-aspnet-web-api/_static/image4.png)

<span data-ttu-id="a3bd3-151">Sol bölmedeki **Test** ' i seçin ve proje türü Için **birim testi projesi** ' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-151">Select **Test** in the left pane, and select **Unit Test Project** for the project type.</span></span> <span data-ttu-id="a3bd3-152">Projeyi **Storeapp. Tests**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-152">Name the project **StoreApp.Tests**.</span></span>

![birim testi projesi Ekle](unit-testing-with-aspnet-web-api/_static/image5.png)

<span data-ttu-id="a3bd3-154">Çözümünüzde birim testi projesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-154">You will see the unit test project in your solution.</span></span>

<span data-ttu-id="a3bd3-155">Birim testi projesinde, özgün projeye bir proje başvurusu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-155">In the unit test project, add a project reference to the original project.</span></span>

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a><span data-ttu-id="a3bd3-156">Web API 2 uygulamasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="a3bd3-156">Set up the Web API 2 application</span></span>

<span data-ttu-id="a3bd3-157">StoreApp projenizde, **Product.cs**adlı **modeller** klasörüne bir sınıf dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-157">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="a3bd3-158">Dosyanın içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-158">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="a3bd3-159">Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-159">Build the solution.</span></span>

<span data-ttu-id="a3bd3-160">Denetleyiciler klasörüne sağ tıklayın ve **Ekle** ve **yeni yapı iskelesi öğesi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-160">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="a3bd3-161">**Web API 2 denetleyici-boş**seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-161">Select **Web API 2 Controller - Empty**.</span></span>

![Yeni denetleyici Ekle](unit-testing-with-aspnet-web-api/_static/image6.png)

<span data-ttu-id="a3bd3-163">Denetleyici adını **Simpleproductcontroller**olarak ayarlayın ve **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-163">Set the controller name to **SimpleProductController**, and click **Add**.</span></span>

![denetleyiciyi belirtin](unit-testing-with-aspnet-web-api/_static/image7.png)

<span data-ttu-id="a3bd3-165">Mevcut kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-165">Replace the existing code with the following code.</span></span> <span data-ttu-id="a3bd3-166">Bu örneği basitleştirmek için, veriler veritabanı yerine bir listede depolanır.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-166">To simplify this example, the data is stored in a list rather than a database.</span></span> <span data-ttu-id="a3bd3-167">Bu sınıfta tanımlanan liste üretim verilerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-167">The list defined in this class represents the production data.</span></span> <span data-ttu-id="a3bd3-168">Denetleyicinin, ürün nesnelerinin listesini parametre olarak alan bir Oluşturucu içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-168">Notice that the controller includes a constructor that takes as a parameter a list of Product objects.</span></span> <span data-ttu-id="a3bd3-169">Bu Oluşturucu, birim testi sırasında test verilerini geçirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-169">This constructor enables you to pass test data when unit testing.</span></span> <span data-ttu-id="a3bd3-170">Denetleyici Ayrıca, zaman uyumsuz yöntemleri birim testi göstermek için iki **zaman uyumsuz** yöntem içerir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-170">The controller also includes two **async** methods to illustrate unit testing asynchronous methods.</span></span> <span data-ttu-id="a3bd3-171">Bu zaman uyumsuz yöntemler, gereksiz kodu en aza indirmek için **Task. FromResult** çağırarak uygulanmıştır, ancak normalde Yöntemler Kaynak yoğunluklu işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-171">These async methods were implemented by calling **Task.FromResult** to minimize extraneous code, but normally the methods would include resource-intensive operations.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="a3bd3-172">GetProduct yöntemi **ıhttpactionresult** arabiriminin bir örneğini döndürür.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-172">The GetProduct method returns an instance of the **IHttpActionResult** interface.</span></span> <span data-ttu-id="a3bd3-173">Ihttpactionresult, Web API 2 ' deki yeni özelliklerden biridir ve birim testi geliştirmeyi basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-173">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span> <span data-ttu-id="a3bd3-174">Ihttpactionresult arabirimini uygulayan sınıflar [System. Web. http. Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) ad alanında bulunur.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-174">Classes that implement the IHttpActionResult interface are found in the [System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) namespace.</span></span> <span data-ttu-id="a3bd3-175">Bu sınıflar bir eylem isteğinden olası yanıtları temsil eder ve HTTP durum kodlarına karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-175">These classes represent possible responses from an action request, and they correspond to HTTP status codes.</span></span>

<span data-ttu-id="a3bd3-176">Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-176">Build the solution.</span></span>

<span data-ttu-id="a3bd3-177">Şimdi test projesi ayarlamaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-177">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="a3bd3-178">NuGet paketlerini test projesine yükler</span><span class="sxs-lookup"><span data-stu-id="a3bd3-178">Install NuGet packages in test project</span></span>

<span data-ttu-id="a3bd3-179">Bir uygulama oluşturmak için boş şablonu kullandığınızda, birim testi projesi (StoreApp. Tests) yüklü herhangi bir NuGet paketini içermez.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-179">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="a3bd3-180">Web API şablonu gibi diğer şablonlar, birim testi projesine bazı NuGet paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-180">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="a3bd3-181">Bu öğretici için, test projesine Microsoft ASP.NET Web API 2 Core paketini dahil etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-181">For this tutorial, you must include the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="a3bd3-182">StoreApp. Tests projesine sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-182">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="a3bd3-183">Paketleri bu projeye eklemek için StoreApp. Tests projesini seçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-183">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![Paketleri yönetme](unit-testing-with-aspnet-web-api/_static/image8.png)

<span data-ttu-id="a3bd3-185">Microsoft ASP.NET Web API 2 çekirdek paketini bulun ve yükler.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-185">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![Web API Core paketini yükler](unit-testing-with-aspnet-web-api/_static/image9.png)

<span data-ttu-id="a3bd3-187">NuGet Paketlerini Yönet penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-187">Close the Manage NuGet Packages window.</span></span>

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="a3bd3-188">Test oluştur</span><span class="sxs-lookup"><span data-stu-id="a3bd3-188">Create tests</span></span>

<span data-ttu-id="a3bd3-189">Varsayılan olarak, test projeniz UnitTest1.cs adlı boş bir test dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-189">By default, your test project includes an empty test file named UnitTest1.cs.</span></span> <span data-ttu-id="a3bd3-190">Bu dosya, test yöntemleri oluşturmak için kullandığınız öznitelikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-190">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="a3bd3-191">Birim testleriniz için bu dosyayı kullanabilir ya da kendi dosyanızı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-191">For your unit tests, you can either use this file or create your own file.</span></span>

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

<span data-ttu-id="a3bd3-193">Bu öğretici için kendi test sınıfınızı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-193">For this tutorial, you will create your own test class.</span></span> <span data-ttu-id="a3bd3-194">UnitTest1.cs dosyasını silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-194">You can delete the UnitTest1.cs file.</span></span> <span data-ttu-id="a3bd3-195">**TestSimpleProductController.cs**adlı bir sınıf ekleyin ve kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-195">Add a class named **TestSimpleProductController.cs**, and replace the code with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="a3bd3-196">Testleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a3bd3-196">Run tests</span></span>

<span data-ttu-id="a3bd3-197">Şimdi testleri çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-197">You are now ready to run the tests.</span></span> <span data-ttu-id="a3bd3-198">**TestMethod** özniteliğiyle işaretlenen tüm yöntem test edilecek.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-198">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="a3bd3-199">**Test** menü öğesinden testleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-199">From the **Test** menu item, run the tests.</span></span>

![testleri çalıştırma](unit-testing-with-aspnet-web-api/_static/image11.png)

<span data-ttu-id="a3bd3-201">**Test Gezgini** penceresini açın ve testlerin sonuçlarına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-201">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![test sonuçları](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a><span data-ttu-id="a3bd3-203">Özet</span><span class="sxs-lookup"><span data-stu-id="a3bd3-203">Summary</span></span>

<span data-ttu-id="a3bd3-204">Bu öğreticiyi tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-204">You have completed this tutorial.</span></span> <span data-ttu-id="a3bd3-205">Bu öğreticideki verilerin birim testi koşullarına odaklanmak için bilerek basitleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a3bd3-205">The data in this tutorial was intentionally simplified to focus on unit testing conditions.</span></span> <span data-ttu-id="a3bd3-206">Birim testi daha gelişmiş veri senaryoları için bkz. [ASP.NET Web API 2 birim testi sırasında Mocking Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="a3bd3-206">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
