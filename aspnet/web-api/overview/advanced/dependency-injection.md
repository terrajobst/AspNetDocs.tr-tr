---
uid: web-api/overview/advanced/dependency-injection
title: ASP.NET Web API 2-ASP.NET 4. x içinde bağımlılık ekleme
author: MikeWasson
description: Bu öğreticide, ASP.NET 4. x için ASP.NET Web API denetleyicinize bağımlılık ekleme gösterilmektedir.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: f9c212af92168ac02644625b9aa8ec1bef329cab
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600418"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="9b920-103">ASP.NET Web API 2 ' de bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="9b920-103">Dependency Injection in ASP.NET Web API 2</span></span>

<span data-ttu-id="9b920-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9b920-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="9b920-105">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="9b920-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="9b920-106">Bu öğreticide, ASP.NET Web API denetleyicinize bağımlılık ekleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9b920-106">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9b920-107">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="9b920-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="9b920-108">Web API 2</span><span class="sxs-lookup"><span data-stu-id="9b920-108">Web API 2</span></span>
> - [<span data-ttu-id="9b920-109">Unity uygulama bloğu</span><span class="sxs-lookup"><span data-stu-id="9b920-109">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="9b920-110">Entity Framework 6 (sürüm 5 de kullanılabilir)</span><span class="sxs-lookup"><span data-stu-id="9b920-110">Entity Framework 6 (version 5 also works)</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="9b920-111">Bağımlılık ekleme nedir?</span><span class="sxs-lookup"><span data-stu-id="9b920-111">What is Dependency Injection?</span></span>

<span data-ttu-id="9b920-112">*Bağımlılık* , başka bir nesnenin gerektirdiği herhangi bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="9b920-112">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="9b920-113">Örneğin, veri erişimini işleyen bir [Depo](http://martinfowler.com/eaaCatalog/repository.html) tanımlanması yaygındır.</span><span class="sxs-lookup"><span data-stu-id="9b920-113">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="9b920-114">Bir örnekle bakalım.</span><span class="sxs-lookup"><span data-stu-id="9b920-114">Let's illustrate with an example.</span></span> <span data-ttu-id="9b920-115">İlk olarak, bir etki alanı modeli tanımlayacağız:</span><span class="sxs-lookup"><span data-stu-id="9b920-115">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="9b920-116">İşte, Entity Framework kullanarak bir veritabanındaki öğeleri depolayan basit bir depo sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9b920-116">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="9b920-117">Şimdi `Product` varlıkları için GET isteklerini destekleyen bir Web API denetleyicisi tanımlayalim.</span><span class="sxs-lookup"><span data-stu-id="9b920-117">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="9b920-118">(Basitlik için GÖNDERI ve diğer yöntemleri dışarıda bırakıyorum.) İlk deneme aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9b920-118">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="9b920-119">Denetleyici sınıfının `ProductRepository`bağlı olduğuna dikkat edin ve denetleyicinin `ProductRepository` örneğini oluşturmasına izin veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="9b920-119">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="9b920-120">Bununla birlikte, birkaç nedenden dolayı bağımlılığı bu şekilde sabit olarak kodladığı için kötü bir fikir olabilir.</span><span class="sxs-lookup"><span data-stu-id="9b920-120">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="9b920-121">`ProductRepository` farklı bir uygulamayla değiştirmek istiyorsanız, denetleyici sınıfını da değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b920-121">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="9b920-122">`ProductRepository` bağımlılıkları varsa, bunları denetleyicinin içinde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b920-122">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="9b920-123">Birden çok denetleyici içeren büyük bir proje için yapılandırma kodunuz projenize dağılmış hale gelir.</span><span class="sxs-lookup"><span data-stu-id="9b920-123">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="9b920-124">Denetleyici, veritabanını sorgulamak için sabit kodlanmış olduğundan, birim testi zordur.</span><span class="sxs-lookup"><span data-stu-id="9b920-124">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="9b920-125">Birim testi için, geçerli tasarımla mümkün olmayan bir sahte veya saplama deposu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b920-125">For a unit test, you should use a mock or stub repository, which is not possible with the current design.</span></span>

<span data-ttu-id="9b920-126">Bu sorunları, depoyu denetleyiciye *ekleme* göre ele alabilir.</span><span class="sxs-lookup"><span data-stu-id="9b920-126">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="9b920-127">İlk olarak, `ProductRepository` sınıfını bir arabirim olarak yeniden düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="9b920-127">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="9b920-128">Sonra `IProductRepository` Oluşturucu parametresi olarak sağlayın:</span><span class="sxs-lookup"><span data-stu-id="9b920-128">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="9b920-129">Bu örnek, [Oluşturucu Ekleme](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)kullanır.</span><span class="sxs-lookup"><span data-stu-id="9b920-129">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="9b920-130">Ayrıca, bir ayarlayıcı yöntemi veya özelliği aracılığıyla bağımlılığı ayarladığınız *ayarlayıcı ekleme*özelliğini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b920-130">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="9b920-131">Ancak artık, uygulamanız denetleyiciyi doğrudan oluşturmadığından bir sorun oluştu.</span><span class="sxs-lookup"><span data-stu-id="9b920-131">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="9b920-132">Web API 'SI isteği yönlendirdiğinizde denetleyiciyi oluşturur ve Web API `IProductRepository`hakkında hiçbir şey bilmez.</span><span class="sxs-lookup"><span data-stu-id="9b920-132">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="9b920-133">Bu, Web API bağımlılığı Çözümleyicisinin geldiği yerdir.</span><span class="sxs-lookup"><span data-stu-id="9b920-133">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="9b920-134">Web API bağımlılığı Çözümleyicisi</span><span class="sxs-lookup"><span data-stu-id="9b920-134">The Web API Dependency Resolver</span></span>

<span data-ttu-id="9b920-135">Web API 'SI, bağımlılıkları çözümlemek için **ıdependencyresolver** arabirimini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9b920-135">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="9b920-136">Arabirimin tanımı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="9b920-136">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="9b920-137">**IDependencyScope** arabirimi iki yönteme sahiptir:</span><span class="sxs-lookup"><span data-stu-id="9b920-137">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="9b920-138">**GetService** bir türün bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9b920-138">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="9b920-139">**GetServices** , belirtilen türde nesnelerin bir koleksiyonunu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9b920-139">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="9b920-140">**Idependencyresolver** yöntemi **IDependencyScope** devralır ve **BeginScope** metodunu ekler.</span><span class="sxs-lookup"><span data-stu-id="9b920-140">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="9b920-141">Bu öğreticide daha sonra kapsamlar hakkında konuşacağız.</span><span class="sxs-lookup"><span data-stu-id="9b920-141">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="9b920-142">Web API 'SI bir denetleyici örneği oluşturduğunda, önce denetleyici türünü geçirerek **ıdependencyresolver. GetService**öğesini çağırır.</span><span class="sxs-lookup"><span data-stu-id="9b920-142">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="9b920-143">Bu genişletilebilirlik kancasını, denetleyiciyi oluşturmak ve tüm bağımlılıkları çözmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b920-143">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="9b920-144">**GetService** null döndürürse, Web API 'si denetleyici sınıfında parametresiz bir oluşturucu arar.</span><span class="sxs-lookup"><span data-stu-id="9b920-144">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="9b920-145">Unity kapsayıcısı ile bağımlılık çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="9b920-145">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="9b920-146">Sıfırdan tamamlanmış bir **ıdependencyresolver** uygulaması yazabilseniz de, arabirim aslında Web API 'si ve var olan IOC kapsayıcıları arasında köprü olarak çalışacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9b920-146">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="9b920-147">Bir IOC kapsayıcısı, bağımlılıkları yönetmekten sorumlu bir yazılım bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="9b920-147">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="9b920-148">Türleri kapsayıcıya kaydeder ve sonra nesneleri oluşturmak için kapsayıcıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9b920-148">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="9b920-149">Kapsayıcı, bağımlılık ilişkilerini otomatik olarak belirler.</span><span class="sxs-lookup"><span data-stu-id="9b920-149">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="9b920-150">Birçok IOC kapsayıcısı ayrıca nesne ömrü ve kapsamı gibi şeyleri denetlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9b920-150">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="9b920-151">"IoC", bir çerçevenin uygulama koduna çağırdığı genel bir model olan "denetimin INVERSION" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9b920-151">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="9b920-152">Bir IOC kapsayıcısı, nesnelerinizi sizin için oluşturur, bu da normal denetim akışını "tersine çevirir".</span><span class="sxs-lookup"><span data-stu-id="9b920-152">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

<span data-ttu-id="9b920-153">Bu öğreticide, Microsoft düzenleri &amp; uygulamalarından [Unity](https://msdn.microsoft.com/library/ff647202.aspx) kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="9b920-153">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="9b920-154">(Diğer popüler kitaplıklar, [role](http://www.castleproject.org/) [Spring.net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [neklemesine](http://www.ninject.org/)ve [StructureMap](http://structuremap.github.io/documentation/)içerir.) Unity 'yi yüklemek için NuGet paket yöneticisini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b920-154">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://structuremap.github.io/documentation/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="9b920-155">Visual Studio 'daki **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="9b920-155">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="9b920-156">Paket Yöneticisi konsolu penceresinde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="9b920-156">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="9b920-157">Bir Unity kapsayıcısını sarmalayan **ıdependencyresolver** 'ın bir uygulaması aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9b920-157">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="9b920-158">**GetService** yöntemi bir türü çözümleyemezse **null**döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="9b920-158">If the **GetService** method cannot resolve a type, it should return **null**.</span></span> <span data-ttu-id="9b920-159">**GetServices** yöntemi bir türü çözümleyemezse boş bir koleksiyon nesnesi döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="9b920-159">If the **GetServices** method cannot resolve a type, it should return an empty collection object.</span></span> <span data-ttu-id="9b920-160">Bilinmeyen türler için özel durumlar oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="9b920-160">Don't throw exceptions for unknown types.</span></span>

## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="9b920-161">Bağımlılık çözümleyici 'yi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9b920-161">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="9b920-162">Genel **HttpConfiguration** nesnesinin **dependencyresolver** özelliğinde bağımlılık çözümleyici 'yi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9b920-162">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="9b920-163">Aşağıdaki kod `IProductRepository` arabirimini Unity 'ye kaydeder ve sonra bir `UnityResolver`oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9b920-163">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="9b920-164">Bağımlılık kapsamı ve denetleyici ömrü</span><span class="sxs-lookup"><span data-stu-id="9b920-164">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="9b920-165">Denetleyiciler istek başına oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9b920-165">Controllers are created per request.</span></span> <span data-ttu-id="9b920-166">**Idependencyresolver** nesne ömrünü yönetmek için bir *kapsamın*kavramını kullanır.</span><span class="sxs-lookup"><span data-stu-id="9b920-166">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="9b920-167">**HttpConfiguration** nesnesine eklenen bağımlılık Çözümleyicisi genel kapsama sahip.</span><span class="sxs-lookup"><span data-stu-id="9b920-167">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="9b920-168">Web API 'SI bir denetleyici oluşturduğunda, **BeginScope**'u çağırır.</span><span class="sxs-lookup"><span data-stu-id="9b920-168">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="9b920-169">Bu yöntem, bir alt kapsamı temsil eden bir **IDependencyScope** döndürür.</span><span class="sxs-lookup"><span data-stu-id="9b920-169">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="9b920-170">Daha sonra Web API 'SI, denetleyiciyi oluşturmak için alt kapsamdaki **GetService** 'i çağırır.</span><span class="sxs-lookup"><span data-stu-id="9b920-170">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="9b920-171">İstek tamamlandığında, Web API 'SI alt kapsamda **Dispose** çağırır.</span><span class="sxs-lookup"><span data-stu-id="9b920-171">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="9b920-172">Denetleyicinin bağımlılıklarını atmak için **Dispose** yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9b920-172">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="9b920-173">**BeginScope** 'ı nasıl uygulayacağınızı IOC kapsayıcısına göre değişir.</span><span class="sxs-lookup"><span data-stu-id="9b920-173">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="9b920-174">Unity için, kapsam bir alt kapsayıcıya karşılık gelir:</span><span class="sxs-lookup"><span data-stu-id="9b920-174">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="9b920-175">Çoğu IOC kapsayıcısının benzer eşdeğerleri vardır.</span><span class="sxs-lookup"><span data-stu-id="9b920-175">Most IoC containers have similar equivalents.</span></span>
