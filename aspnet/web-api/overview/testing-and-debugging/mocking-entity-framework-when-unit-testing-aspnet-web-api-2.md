---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: Birim testi ASP.NET Web API 2 ' de Entity Framework Mocking | Microsoft Docs
author: Rick-Anderson
description: Bu kılavuz ve uygulama, Entity Framework kullanan Web API 2 uygulamanız için birim testlerinin nasıl oluşturulacağını göstermektedir. Nasıl değiştirileceği gösterilmektedir...
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555092"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a><span data-ttu-id="f6c96-104">Birim testi ASP.NET Web API 2 ' de Entity Framework Mocking</span><span class="sxs-lookup"><span data-stu-id="f6c96-104">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="f6c96-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="f6c96-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="f6c96-106">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="f6c96-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="f6c96-107">Bu kılavuz ve uygulama, Entity Framework kullanan Web API 2 uygulamanız için birim testlerinin nasıl oluşturulacağını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="f6c96-107">This guidance and application demonstrate how to create unit tests for your Web API 2 application that uses the Entity Framework.</span></span> <span data-ttu-id="f6c96-108">Bağlam nesnesinin test için geçirilmesini ve Entity Framework birlikte çalışan test nesnelerinin nasıl oluşturulacağını etkinleştirmek için, yapı iskelesi denetleyicisinin nasıl değiştirileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6c96-108">It shows how to modify the scaffolded controller to enable passing a context object for testing, and how to create test objects that work with Entity Framework.</span></span>
>
> <span data-ttu-id="f6c96-109">ASP.NET Web API 'SI ile birim teste giriş için bkz. [ASP.NET Web API 2 Ile birim testi](unit-testing-with-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="f6c96-109">For an introduction to unit testing with ASP.NET Web API, see [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md).</span></span>
>
> <span data-ttu-id="f6c96-110">Bu öğreticide, ASP.NET Web API 'sinin temel kavramları hakkında bilgi sahibi olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="f6c96-110">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="f6c96-111">Tanıtım öğreticisi için bkz. [ASP.NET Web API 2 Ile çalışmaya](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)başlama.</span><span class="sxs-lookup"><span data-stu-id="f6c96-111">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f6c96-112">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="f6c96-112">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="f6c96-113">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f6c96-113">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="f6c96-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="f6c96-114">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="f6c96-115">Bu konuda</span><span class="sxs-lookup"><span data-stu-id="f6c96-115">In this topic</span></span>

<span data-ttu-id="f6c96-116">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="f6c96-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="f6c96-117">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f6c96-117">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="f6c96-118">Kodu indir</span><span class="sxs-lookup"><span data-stu-id="f6c96-118">Download code</span></span>](#download)
- [<span data-ttu-id="f6c96-119">Birim testi projesiyle uygulama oluştur</span><span class="sxs-lookup"><span data-stu-id="f6c96-119">Create application with unit test project</span></span>](#appwithunittest)
- [<span data-ttu-id="f6c96-120">Model sınıfı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f6c96-120">Create the model class</span></span>](#modelclass)
- [<span data-ttu-id="f6c96-121">Denetleyiciyi ekleme</span><span class="sxs-lookup"><span data-stu-id="f6c96-121">Add the controller</span></span>](#controller)
- [<span data-ttu-id="f6c96-122">Bağımlılık ekleme ekleme</span><span class="sxs-lookup"><span data-stu-id="f6c96-122">Add dependency injection</span></span>](#dependency)
- [<span data-ttu-id="f6c96-123">NuGet paketlerini test projesine yükler</span><span class="sxs-lookup"><span data-stu-id="f6c96-123">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="f6c96-124">Test bağlamı oluştur</span><span class="sxs-lookup"><span data-stu-id="f6c96-124">Create test context</span></span>](#testcontext)
- [<span data-ttu-id="f6c96-125">Test oluştur</span><span class="sxs-lookup"><span data-stu-id="f6c96-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="f6c96-126">Testleri Çalıştır</span><span class="sxs-lookup"><span data-stu-id="f6c96-126">Run tests</span></span>](#runtests)

<span data-ttu-id="f6c96-127">[ASP.NET Web API 2 Ile birim testinde](unit-testing-with-aspnet-web-api.md)adımları zaten tamamladıysanız, [denetleyiciyi ekleme](#controller)bölümüne atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6c96-127">If you have already completed the steps in [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), you can skip to the section [Add the controller](#controller).</span></span>

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="f6c96-128">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f6c96-128">Prerequisites</span></span>

<span data-ttu-id="f6c96-129">Visual Studio 2017 Community, Professional veya Enterprise Edition</span><span class="sxs-lookup"><span data-stu-id="f6c96-129">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="f6c96-130">Kodu indirin</span><span class="sxs-lookup"><span data-stu-id="f6c96-130">Download code</span></span>

<span data-ttu-id="f6c96-131">[Tamamlanmış projeyi](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)indirin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-131">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="f6c96-132">İndirilebilir proje, bu konu için birim test kodu ve [birim testi ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) konusu için içerir.</span><span class="sxs-lookup"><span data-stu-id="f6c96-132">The downloadable project includes unit test code for this topic and for the [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="f6c96-133">Birim testi projesiyle uygulama oluştur</span><span class="sxs-lookup"><span data-stu-id="f6c96-133">Create application with unit test project</span></span>

<span data-ttu-id="f6c96-134">Uygulamanızı oluştururken bir birim testi projesi oluşturabilir veya var olan bir uygulamaya bir birim testi projesi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6c96-134">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="f6c96-135">Bu öğretici, uygulamayı oluştururken bir birim testi projesi oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6c96-135">This tutorial shows creating a unit test project when creating the application.</span></span>

<span data-ttu-id="f6c96-136">**Storeapp**adlı yeni bir ASP.NET Web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f6c96-136">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

<span data-ttu-id="f6c96-137">Yeni ASP.NET proje penceresinde **boş** şablonu seçin ve Web API 'si için klasörler ve çekirdek başvurular ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-137">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="f6c96-138">**Birim testleri Ekle** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-138">Select the **Add unit tests** option.</span></span> <span data-ttu-id="f6c96-139">Birim testi projesi, otomatik olarak **Storeapp. Tests**olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="f6c96-139">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="f6c96-140">Bu adı koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6c96-140">You can keep this name.</span></span>

![birim testi projesi oluştur](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

<span data-ttu-id="f6c96-142">Uygulamayı oluşturduktan sonra, bunu iki proje- **Storeapp** ve **Storeapp. Tests**içerdiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f6c96-142">After creating the application, you will see it contains two projects - **StoreApp** and **StoreApp.Tests**.</span></span>

<a id="modelclass"></a>
## <a name="create-the-model-class"></a><span data-ttu-id="f6c96-143">Model sınıfı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f6c96-143">Create the model class</span></span>

<span data-ttu-id="f6c96-144">StoreApp projenizde, **Product.cs**adlı **modeller** klasörüne bir sınıf dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-144">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="f6c96-145">Dosyanın içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-145">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

<span data-ttu-id="f6c96-146">Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-146">Build the solution.</span></span>

<a id="controller"></a>
## <a name="add-the-controller"></a><span data-ttu-id="f6c96-147">Denetleyiciyi ekleme</span><span class="sxs-lookup"><span data-stu-id="f6c96-147">Add the controller</span></span>

<span data-ttu-id="f6c96-148">Denetleyiciler klasörüne sağ tıklayın ve **Ekle** ve **yeni yapı iskelesi öğesi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-148">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="f6c96-149">Entity Framework kullanarak, eylemlerle Web API 2 denetleyicisi ' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-149">Select Web API 2 Controller with actions, using Entity Framework.</span></span>

![Yeni denetleyici Ekle](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

<span data-ttu-id="f6c96-151">Aşağıdaki değerleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="f6c96-151">Set the following values:</span></span>

- <span data-ttu-id="f6c96-152">Denetleyici adı: **ProductController**</span><span class="sxs-lookup"><span data-stu-id="f6c96-152">Controller name: **ProductController**</span></span>
- <span data-ttu-id="f6c96-153">Model Sınıfı: **ürün**</span><span class="sxs-lookup"><span data-stu-id="f6c96-153">Model class: **Product**</span></span>
- <span data-ttu-id="f6c96-154">Veri bağlamı sınıfı: [aşağıda görülen değerleri dolduran **Yeni veri bağlam** düğmesini seçin]</span><span class="sxs-lookup"><span data-stu-id="f6c96-154">Data context class: [Select **New data context** button which fills in the values seen below]</span></span>

![denetleyiciyi belirtin](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

<span data-ttu-id="f6c96-156">Denetleyiciyi otomatik olarak oluşturulan kodla oluşturmak için **Ekle** ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f6c96-156">Click **Add** to create the controller with automatically-generated code.</span></span> <span data-ttu-id="f6c96-157">Kod, ürün sınıfının örneklerini oluşturma, alma, güncelleştirme ve silme yöntemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="f6c96-157">The code includes methods for creating, retrieving, updating and deleting instances of the Product class.</span></span> <span data-ttu-id="f6c96-158">Aşağıdaki kod, ürün ekleme yöntemini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6c96-158">The following code shows the method for add a Product.</span></span> <span data-ttu-id="f6c96-159">Metodun bir **ıhttpactionresult**örneği döndürtiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-159">Notice that the method returns an instance of **IHttpActionResult**.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

<span data-ttu-id="f6c96-160">Ihttpactionresult, Web API 2 ' deki yeni özelliklerden biridir ve birim testi geliştirmeyi basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="f6c96-160">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span>

<span data-ttu-id="f6c96-161">Bir sonraki bölümde, test nesnelerini denetleyiciye geçirmeyi kolaylaştırmak için oluşturulan kodu özelleştirecek olursunuz.</span><span class="sxs-lookup"><span data-stu-id="f6c96-161">In the next section, you will customize the generated code to facilitate passing test objects to the controller.</span></span>

<a id="dependency"></a>
## <a name="add-dependency-injection"></a><span data-ttu-id="f6c96-162">Bağımlılık ekleme ekleme</span><span class="sxs-lookup"><span data-stu-id="f6c96-162">Add dependency injection</span></span>

<span data-ttu-id="f6c96-163">Şu anda, ProductController sınıfı StoreAppContext sınıfının bir örneğini kullanmak için sabit olarak kodlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f6c96-163">Currently, the ProductController class is hard-coded to use an instance of the StoreAppContext class.</span></span> <span data-ttu-id="f6c96-164">Uygulamanızı değiştirmek ve bu sabit kodlanmış bağımlılığı kaldırmak için bağımlılık ekleme adlı bir model kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f6c96-164">You will use a pattern called dependency injection to modify your application and remove that hard-coded dependency.</span></span> <span data-ttu-id="f6c96-165">Bu bağımlılığı bozarak, test ederken bir sahte nesne geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6c96-165">By breaking this dependency, you can pass in a mock object when testing.</span></span>

<span data-ttu-id="f6c96-166">**Modeller** klasörüne sağ tıklayın ve **Istoreappcontext**adlı yeni bir arabirim ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-166">Right-click the **Models** folder, and add a new interface named **IStoreAppContext**.</span></span>

<span data-ttu-id="f6c96-167">Kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-167">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

<span data-ttu-id="f6c96-168">StoreAppContext.cs dosyasını açın ve aşağıdaki vurgulanan değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="f6c96-168">Open the StoreAppContext.cs file and make the following highlighted changes.</span></span> <span data-ttu-id="f6c96-169">Nottaki önemli değişiklikler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f6c96-169">The important changes to note are:</span></span>

- <span data-ttu-id="f6c96-170">StoreAppContext sınıfı ıtoreappcontext arabirimini uygular</span><span class="sxs-lookup"><span data-stu-id="f6c96-170">StoreAppContext class implements IStoreAppContext interface</span></span>
- <span data-ttu-id="f6c96-171">MarkAsModified yöntemi uygulandı</span><span class="sxs-lookup"><span data-stu-id="f6c96-171">MarkAsModified method is implemented</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

<span data-ttu-id="f6c96-172">ProductController.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="f6c96-172">Open the ProductController.cs file.</span></span> <span data-ttu-id="f6c96-173">Mevcut kodu vurgulanan kodla eşleşecek şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-173">Change the existing code to match the highlighted code.</span></span> <span data-ttu-id="f6c96-174">Bu değişiklikler StoreAppContext üzerindeki bağımlılığı keser ve diğer sınıfların bağlam sınıfı için farklı bir nesneye geçmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f6c96-174">These changes break the dependency on StoreAppContext and enable other classes to pass in a different object for the context class.</span></span> <span data-ttu-id="f6c96-175">Bu değişiklik, birim testleri sırasında bir test bağlamı geçirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f6c96-175">This change will enable you to pass in a test context during unit tests.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

<span data-ttu-id="f6c96-176">ProductController 'da yapmanız gereken bir değişiklik daha vardır.</span><span class="sxs-lookup"><span data-stu-id="f6c96-176">There is one more change you must make in ProductController.</span></span> <span data-ttu-id="f6c96-177">**Putproduct** yönteminde, varlık durumunu ayarlayan satırı, MarkAsModified yöntemine yapılan bir çağrı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-177">In the **PutProduct** method, replace the line that sets the entity state to modified with a call to the MarkAsModified method.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

<span data-ttu-id="f6c96-178">Çözümü derleyin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-178">Build the solution.</span></span>

<span data-ttu-id="f6c96-179">Şimdi test projesi ayarlamaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="f6c96-179">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="f6c96-180">NuGet paketlerini test projesine yükler</span><span class="sxs-lookup"><span data-stu-id="f6c96-180">Install NuGet packages in test project</span></span>

<span data-ttu-id="f6c96-181">Bir uygulama oluşturmak için boş şablonu kullandığınızda, birim testi projesi (StoreApp. Tests) yüklü herhangi bir NuGet paketini içermez.</span><span class="sxs-lookup"><span data-stu-id="f6c96-181">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="f6c96-182">Web API şablonu gibi diğer şablonlar, birim testi projesine bazı NuGet paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="f6c96-182">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="f6c96-183">Bu öğreticide, Entity Framework paketini ve Microsoft ASP.NET Web API 2 Core paketini test projesine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6c96-183">For this tutorial, you must include the Entity Framework package and the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="f6c96-184">StoreApp. Tests projesine sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-184">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="f6c96-185">Paketleri bu projeye eklemek için StoreApp. Tests projesini seçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="f6c96-185">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![Paketleri yönetme](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

<span data-ttu-id="f6c96-187">Çevrimiçi paketlerden EntityFramework paketini bulun ve (sürüm 6,0 veya üzeri) yükler.</span><span class="sxs-lookup"><span data-stu-id="f6c96-187">From the Online packages, find and install the EntityFramework package (version 6.0 or later).</span></span> <span data-ttu-id="f6c96-188">EntityFramework paketinin zaten yüklü olduğu görüntülenirse StoreApp. Tests projesi yerine StoreApp projesini seçmiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6c96-188">If it appears that the EntityFramework package is already installed, you may have selected the StoreApp project instead of the StoreApp.Tests project.</span></span>

![Entity Framework Ekle](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

<span data-ttu-id="f6c96-190">Microsoft ASP.NET Web API 2 çekirdek paketini bulun ve yükler.</span><span class="sxs-lookup"><span data-stu-id="f6c96-190">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![Web API Core paketini yükler](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

<span data-ttu-id="f6c96-192">NuGet Paketlerini Yönet penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="f6c96-192">Close the Manage NuGet Packages window.</span></span>

<a id="testcontext"></a>
## <a name="create-test-context"></a><span data-ttu-id="f6c96-193">Test bağlamı oluştur</span><span class="sxs-lookup"><span data-stu-id="f6c96-193">Create test context</span></span>

<span data-ttu-id="f6c96-194">Test projesine **Testdbset** adlı bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-194">Add a class named **TestDbSet** to the test project.</span></span> <span data-ttu-id="f6c96-195">Bu sınıf, test veri kümesi için temel sınıf olarak hizmet verir.</span><span class="sxs-lookup"><span data-stu-id="f6c96-195">This class serves as the base class for your test data set.</span></span> <span data-ttu-id="f6c96-196">Kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-196">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

<span data-ttu-id="f6c96-197">Aşağıdaki kodu içeren test projesine **Testproductdbset** adlı bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-197">Add a class named **TestProductDbSet** to the test project which contains the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

<span data-ttu-id="f6c96-198">**Teststoreappcontext** adlı bir sınıf ekleyin ve mevcut kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-198">Add a class named **TestStoreAppContext** and replace the existing code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="f6c96-199">Test oluştur</span><span class="sxs-lookup"><span data-stu-id="f6c96-199">Create tests</span></span>

<span data-ttu-id="f6c96-200">Varsayılan olarak, test projeniz **UnitTest1.cs**adlı boş bir test dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="f6c96-200">By default, your test project includes an empty test file named **UnitTest1.cs**.</span></span> <span data-ttu-id="f6c96-201">Bu dosya, test yöntemleri oluşturmak için kullandığınız öznitelikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6c96-201">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="f6c96-202">Bu öğreticide, yeni bir test sınıfı ekleyeceğiniz için bu dosyayı silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6c96-202">For this tutorial, you can delete this file because you will add a new test class.</span></span>

<span data-ttu-id="f6c96-203">Test projesine **Testproductcontroller** adlı bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-203">Add a class named **TestProductController** to the test project.</span></span> <span data-ttu-id="f6c96-204">Kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-204">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="f6c96-205">Testleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f6c96-205">Run tests</span></span>

<span data-ttu-id="f6c96-206">Şimdi testleri çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="f6c96-206">You are now ready to run the tests.</span></span> <span data-ttu-id="f6c96-207">**TestMethod** özniteliğiyle işaretlenen tüm yöntem test edilecek.</span><span class="sxs-lookup"><span data-stu-id="f6c96-207">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="f6c96-208">**Test** menü öğesinden testleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f6c96-208">From the **Test** menu item, run the tests.</span></span>

![testleri çalıştırma](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

<span data-ttu-id="f6c96-210">**Test Gezgini** penceresini açın ve testlerin sonuçlarına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f6c96-210">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![test sonuçları](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
