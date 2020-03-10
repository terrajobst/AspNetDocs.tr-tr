---
uid: signalr/overview/older-versions/dependency-injection
title: SignalR 1. x 'e bağımlılık ekleme | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: de838ab6b3a299eb1e5ebeb9fa3c583478ce3e56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536955"
---
# <a name="dependency-injection-in-signalr-1x"></a><span data-ttu-id="0f60e-102">SignalR 1.x Sürümünde Bağımlılık Ekleme</span><span class="sxs-lookup"><span data-stu-id="0f60e-102">Dependency Injection in SignalR 1.x</span></span>

<span data-ttu-id="0f60e-103">, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="0f60e-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="0f60e-104">Bağımlılık ekleme, nesneler arasında sabit kodlanmış bağımlılıkları kaldırmanın bir yoludur. bu sayede, bir nesnenin bağımlılıklarını test etmek için (sahte nesneleri kullanarak) veya çalışma zamanı davranışını değiştirmek kolaylaşır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-104">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="0f60e-105">Bu öğreticide, SignalR hub 'larda bağımlılık ekleme işlemlerinin nasıl gerçekleştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-105">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="0f60e-106">Ayrıca, SignalR ile IOC kapsayıcılarını nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-106">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="0f60e-107">Bir IOC kapsayıcısı, bağımlılık ekleme için genel bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-107">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="0f60e-108">Bağımlılık ekleme nedir?</span><span class="sxs-lookup"><span data-stu-id="0f60e-108">What is Dependency Injection?</span></span>

<span data-ttu-id="0f60e-109">Bağımlılık ekleme konusunda zaten bilgi sahibiyseniz bu bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-109">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="0f60e-110">*Bağımlılık ekleme* (dı), nesnelerin kendi bağımlılıklarını oluşturmadan sorumlu olmayan bir modeldir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-110">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="0f60e-111">İşte, bu, bir değer olarak motive etmek için basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-111">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="0f60e-112">İletileri günlüğe kaydetmek için gereken bir nesneniz olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="0f60e-112">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="0f60e-113">Günlüğe kaydetme arabirimi tanımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0f60e-113">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="0f60e-114">Nesneniz, iletileri günlüğe kaydetmek için bir `ILogger` oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0f60e-114">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="0f60e-115">Bu işe yarar, ancak en iyi tasarım değildir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-115">This works, but it's not the best design.</span></span> <span data-ttu-id="0f60e-116">`FileLogger` başka bir `ILogger` uygulamasıyla değiştirmek istiyorsanız `SomeComponent`değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-116">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="0f60e-117">Birçok farklı nesnenin `FileLogger`kullanduymasını, bunların tümünü değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-117">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="0f60e-118">Ya da tek bir `FileLogger` yapmaya karar verirseniz, uygulama genelinde de değişiklikler yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-118">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="0f60e-119">Daha iyi bir yaklaşım, nesne içine bir `ILogger` eklemek — örneğin, bir Oluşturucu bağımsız değişkeni kullanarak:</span><span class="sxs-lookup"><span data-stu-id="0f60e-119">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="0f60e-120">Artık, hangi `ILogger` kullanacağınızı seçmeden nesne sorumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-120">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="0f60e-121">Kendisine bağımlı nesneleri değiştirmeden `ILogger` uygulamaları geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f60e-121">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="0f60e-122">Bu düzene [Oluşturucu Ekleme](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)adı verilir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-122">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="0f60e-123">Başka bir model, bir ayarlayıcı yöntemi veya özelliği aracılığıyla bağımlılığı ayarladığınız ayarlayıcı ekleme işlemi olur.</span><span class="sxs-lookup"><span data-stu-id="0f60e-123">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="0f60e-124">SignalR 'de basit bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="0f60e-124">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="0f60e-125">[SignalR Ile çalışmaya](../getting-started/tutorial-getting-started-with-signalr.md)başlama öğreticiden sohbet uygulamasını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="0f60e-125">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="0f60e-126">Bu uygulamadaki Merkez sınıfı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0f60e-126">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="0f60e-127">Göndermeden önce sohbet iletilerini sunucuda depolamak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="0f60e-127">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="0f60e-128">Bu işlevi soyutlayan bir arabirim tanımlayabilir ve arabirimi `ChatHub` sınıfına eklemek için DI kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f60e-128">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="0f60e-129">Tek sorun, bir SignalR uygulamasının doğrudan hub oluşturmamalıdır; SignalR bunları sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f60e-129">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="0f60e-130">Varsayılan olarak, SignalR bir hub sınıfının parametresiz bir oluşturucuya sahip olmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="0f60e-130">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="0f60e-131">Ancak, hub örnekleri oluşturmak için bir işlevi kolayca kaydedebilir ve bu işlevi, DI işlemini gerçekleştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f60e-131">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="0f60e-132">**Globalhost. DependencyResolver. Register**çağırarak işlevi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0f60e-132">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="0f60e-133">Artık `ChatHub` bir örnek oluşturması gerektiğinde SignalR bu anonim işlevi çağıracaktır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-133">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="0f60e-134">IoC kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="0f60e-134">IoC Containers</span></span>

<span data-ttu-id="0f60e-135">Önceki kod, basit durumlar için uygundur.</span><span class="sxs-lookup"><span data-stu-id="0f60e-135">The previous code is fine for simple cases.</span></span> <span data-ttu-id="0f60e-136">Ancak yine de şunu yazmanız gerekiyordu:</span><span class="sxs-lookup"><span data-stu-id="0f60e-136">But you still had to write this:</span></span>

[!code-css[Main](dependency-injection/samples/sample8.css)]

<span data-ttu-id="0f60e-137">Birçok bağımlılığı olan karmaşık bir uygulamada, bu "kablolama" kodunun çoğunu yazmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-137">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="0f60e-138">Özellikle bağımlılıklar iç içe ise, bu kod bakımını yapmak zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-138">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="0f60e-139">Ayrıca birim testi de zordur.</span><span class="sxs-lookup"><span data-stu-id="0f60e-139">It is also hard to unit test.</span></span>

<span data-ttu-id="0f60e-140">Bir çözüm bir IOC kapsayıcısı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-140">One solution is to use an IoC container.</span></span> <span data-ttu-id="0f60e-141">Bir IOC kapsayıcısı, bağımlılıkları yönetmekten sorumlu bir yazılım bileşenidir. Türleri kapsayıcıya kaydeder ve sonra nesneleri oluşturmak için kapsayıcıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-141">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="0f60e-142">Kapsayıcı, bağımlılık ilişkilerini otomatik olarak belirler.</span><span class="sxs-lookup"><span data-stu-id="0f60e-142">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="0f60e-143">Birçok IOC kapsayıcısı ayrıca nesne ömrü ve kapsamı gibi şeyleri denetlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-143">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="0f60e-144">"IoC", bir çerçevenin uygulama koduna çağırdığı genel bir model olan "denetimin INVERSION" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-144">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="0f60e-145">Bir IOC kapsayıcısı, nesnelerinizi sizin için oluşturur, bu da normal denetim akışını "tersine çevirir".</span><span class="sxs-lookup"><span data-stu-id="0f60e-145">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="0f60e-146">SignalR 'de IOC kapsayıcıları kullanma</span><span class="sxs-lookup"><span data-stu-id="0f60e-146">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="0f60e-147">Sohbet uygulaması, bir IOC kapsayıcısından faydalanmak için büyük olasılıkla çok basittir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-147">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="0f60e-148">Bunun yerine [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) örneğine göz atalım.</span><span class="sxs-lookup"><span data-stu-id="0f60e-148">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="0f60e-149">StockTicker örneği iki ana sınıfı tanımlar:</span><span class="sxs-lookup"><span data-stu-id="0f60e-149">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="0f60e-150">`StockTickerHub`: istemci bağlantılarını yöneten hub sınıfı.</span><span class="sxs-lookup"><span data-stu-id="0f60e-150">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="0f60e-151">`StockTicker`: stok fiyatlarını tutan ve düzenli aralıklarla güncelleştiren bir tek.</span><span class="sxs-lookup"><span data-stu-id="0f60e-151">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="0f60e-152">`StockTickerHub`, `StockTicker` tekil öğesine bir başvuru tutar `StockTicker` ancak `StockTickerHub`için **IHV Ubconnectioncontext** 'e bir başvuru barındırır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-152">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="0f60e-153">`StockTickerHub` örneklerle iletişim kurmak için bu arabirimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-153">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="0f60e-154">(Daha fazla bilgi için bkz. [ASP.NET SignalR Ile sunucu yayını](index.md).)</span><span class="sxs-lookup"><span data-stu-id="0f60e-154">(For more information, see [Server Broadcast with ASP.NET SignalR](index.md).)</span></span>

<span data-ttu-id="0f60e-155">Bu bağımlılıklara bir bit eklemek için bir IOC kapsayıcısı kullanabiliriz.</span><span class="sxs-lookup"><span data-stu-id="0f60e-155">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="0f60e-156">İlk olarak, `StockTickerHub` ve `StockTicker` sınıflarını basitleşelim.</span><span class="sxs-lookup"><span data-stu-id="0f60e-156">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="0f60e-157">Aşağıdaki kodda, ihtiyaç duyduğumuz parçalar hakkında yorum yaptı.</span><span class="sxs-lookup"><span data-stu-id="0f60e-157">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="0f60e-158">Parametresiz oluşturucuyu `StockTicker`kaldırın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-158">Remove the parameterless constructor from `StockTicker`.</span></span> <span data-ttu-id="0f60e-159">Bunun yerine, her zaman, hub 'ı oluşturmak için DI 'yi kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="0f60e-159">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="0f60e-160">StockTicker için Singleton örneğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-160">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="0f60e-161">Daha sonra, StockTicker ömrünü denetlemek için IoC kapsayıcısını kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="0f60e-161">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="0f60e-162">Ayrıca, oluşturucuyu genel hale getirin.</span><span class="sxs-lookup"><span data-stu-id="0f60e-162">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="0f60e-163">Daha sonra, `StockTicker`için bir arabirim oluşturarak kodu yeniden düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f60e-163">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="0f60e-164">Bu arabirimi, `StockTickerHub` `StockTicker` sınıfından ayırmak için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="0f60e-164">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="0f60e-165">Visual Studio bu tür yeniden düzenleme kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-165">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="0f60e-166">StockTicker.cs dosyasını açın, `StockTicker` sınıfı bildirimine sağ tıklayın ve yeniden **Düzenle** ... seçeneğini belirleyin. **Arabirimi Ayıkla**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-166">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="0f60e-167">**Arabirimi Ayıkla** Iletişim kutusunda **Tümünü Seç**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-167">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="0f60e-168">Diğer varsayılan değerleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-168">Leave the other defaults.</span></span> <span data-ttu-id="0f60e-169">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-169">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="0f60e-170">Visual Studio `IStockTicker`adlı yeni bir arabirim oluşturur ve ayrıca `IStockTicker`türetmeye `StockTicker` değişir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-170">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="0f60e-171">IStockTicker.cs dosyasını açın ve arabirimi **genel**' e değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0f60e-171">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="0f60e-172">`StockTickerHub` sınıfında, iki `StockTicker` örneğini `IStockTicker`olarak değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0f60e-172">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="0f60e-173">`IStockTicker` arabirimi oluşturmak kesinlikle gerekli değildir, ancak uygulamanızın uygulamanızdaki bileşenler arasında Eşleneni azaltmaya nasıl yardımcı olduğunu göstermek istiyorum.</span><span class="sxs-lookup"><span data-stu-id="0f60e-173">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="0f60e-174">Nekleme kitaplığını ekleme</span><span class="sxs-lookup"><span data-stu-id="0f60e-174">Add the Ninject Library</span></span>

<span data-ttu-id="0f60e-175">.NET için çok sayıda açık kaynaklı IFC kapsayıcısı vardır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-175">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="0f60e-176">Bu öğretici için [Nekleme](http://www.ninject.org/)'yi kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="0f60e-176">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="0f60e-177">(Diğer popüler kitaplıklar, [role](http://www.castleproject.org/) [Spring.net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity)ve [StructureMap](http://docs.structuremap.net)içerir.)</span><span class="sxs-lookup"><span data-stu-id="0f60e-177">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="0f60e-178">[Nekleme kitaplığını](https://nuget.org/packages/Ninject/3.0.1.10)yüklemek Için NuGet Paket Yöneticisi 'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-178">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="0f60e-179">Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi** > **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="0f60e-179">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="0f60e-180">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="0f60e-180">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="0f60e-181">SignalR bağımlılık çözümleyicisini değiştirme</span><span class="sxs-lookup"><span data-stu-id="0f60e-181">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="0f60e-182">SignalR içinde Nekleme kullanmak için, **Defaultdependencyresolver**'dan türeyen bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0f60e-182">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="0f60e-183">Bu sınıf, **Defaultdependencyresolver**'ın **GetService** ve **GetServices** yöntemlerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="0f60e-183">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="0f60e-184">SignalR, hub örnekleri ve ayrıca SignalR tarafından dahili olarak kullanılan çeşitli hizmetler dahil olmak üzere çalışma zamanında çeşitli nesneler oluşturmak için bu yöntemleri çağırır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-184">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="0f60e-185">**GetService** yöntemi bir türün tek bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f60e-185">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="0f60e-186">Nekleme çekirdeğinin **TryGet** yöntemini çağırmak için bu yöntemi geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-186">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="0f60e-187">Bu yöntem null döndürürse, varsayılan çözümleyiciye geri dönün.</span><span class="sxs-lookup"><span data-stu-id="0f60e-187">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="0f60e-188">**GetServices** yöntemi, belirtilen türde nesnelerin bir koleksiyonunu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f60e-188">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="0f60e-189">Neklemesine ait sonuçları varsayılan çözümleyiciyle sonuçlarla birleştirmek için bu yöntemi geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-189">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="0f60e-190">Nekleme bağlamalarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0f60e-190">Configure Ninject Bindings</span></span>

<span data-ttu-id="0f60e-191">Şimdi tür bağlamaları bildirmek için Nekleme kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="0f60e-191">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="0f60e-192">RegisterHubs.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-192">Open the file RegisterHubs.cs.</span></span> <span data-ttu-id="0f60e-193">`RegisterHubs.Start` yönteminde Nekleme kapsayıcısını oluşturun ve Nekleme, *çekirdeği*çağırır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-193">In the `RegisterHubs.Start` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="0f60e-194">Özel bağımlılık çözümleyicimizin bir örneğini oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0f60e-194">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="0f60e-195">`IStockTicker` için aşağıdaki şekilde bir bağlama oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0f60e-195">Create a binding for `IStockTicker` as follows:</span></span>

[!code-html[Main](dependency-injection/samples/sample17.html)]

<span data-ttu-id="0f60e-196">Bu kod iki şeyi söyleyerek.</span><span class="sxs-lookup"><span data-stu-id="0f60e-196">This code is saying two things.</span></span> <span data-ttu-id="0f60e-197">İlk olarak, uygulama bir `IStockTicker`ihtiyaç duyduğunda, çekirdek bir `StockTicker`örneği oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-197">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="0f60e-198">İkincisi, `StockTicker` sınıfı tek bir nesne olarak oluşturulmuş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-198">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="0f60e-199">Nekleme nesnenin bir örneğini oluşturur ve her istek için aynı örneği döndürür.</span><span class="sxs-lookup"><span data-stu-id="0f60e-199">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="0f60e-200">**Iubconnectioncontext** için aşağıdaki şekilde bir bağlama oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0f60e-200">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="0f60e-201">Bu kod, bir **Ihubconnection**döndüren anonim bir işlev oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f60e-201">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="0f60e-202">**Whenınjectedinto** yöntemi, neklemesine bu işlevi yalnızca `IStockTicker` örnekleri oluştururken kullanmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="0f60e-202">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="0f60e-203">Bunun nedeni, SignalR 'nin, dahili olarak **IHV Ubconnectioncontext** örnekleri oluşturduğunu ve SignalR 'nin bunları nasıl oluşturduğunu geçersiz kılmak istemedik.</span><span class="sxs-lookup"><span data-stu-id="0f60e-203">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="0f60e-204">Bu işlev yalnızca `StockTicker` sınıfımız için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-204">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="0f60e-205">Bağımlılık çözümleyicisini **Maphubs** yöntemine geçirin:</span><span class="sxs-lookup"><span data-stu-id="0f60e-205">Pass the dependency resolver into the **MapHubs** method:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="0f60e-206">Şimdi SignalR, varsayılan çözümleyici yerine **Maphubs**içinde belirtilen çözümleyiciyi kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-206">Now SignalR will use the resolver specified in **MapHubs**, instead of the default resolver.</span></span>

<span data-ttu-id="0f60e-207">`RegisterHubs.Start`için kod listesinin tamamı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-207">Here is the complete code listing for `RegisterHubs.Start`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="0f60e-208">Visual Studio 'da StockTicker uygulamasını çalıştırmak için F5 'e basın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-208">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="0f60e-209">Tarayıcı penceresinde `http://localhost:*port*/SignalR.Sample/StockTicker.html`' a gidin.</span><span class="sxs-lookup"><span data-stu-id="0f60e-209">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="0f60e-210">Uygulama daha önce olduğu gibi tamamen aynı işlevselliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-210">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="0f60e-211">(Bir açıklama için bkz. [ASP.NET SignalR Ile sunucu yayını](index.md).) Davranışı değiştirmedik; kodu test etmek, sürdürmek ve geliştirmek için daha kolay hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-211">(For a description, see [Server Broadcast with ASP.NET SignalR](index.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
