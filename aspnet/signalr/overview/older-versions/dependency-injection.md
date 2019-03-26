---
uid: signalr/overview/older-versions/dependency-injection
title: Signalr'da bağımlılık ekleme 1.x | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 311976a9d0e79083e02231ab056af3537a3d3d25
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58420809"
---
<a name="dependency-injection-in-signalr-1x"></a><span data-ttu-id="d8f6a-102">SignalR 1.x Sürümünde Bağımlılık Ekleme</span><span class="sxs-lookup"><span data-stu-id="d8f6a-102">Dependency Injection in SignalR 1.x</span></span>
====================
<span data-ttu-id="d8f6a-103">tarafından [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="d8f6a-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="d8f6a-104">Bağımlılık ekleme (sahte nesneler kullanılarak) test etmek için ya da bir nesnenin bağımlılıkları değiştirin veya çalışma zamanı davranışını değiştirmek için daha kolay hale getirme nesneleri arasındaki sabit kodlu bağımlılıkları kaldırmak için bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-104">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="d8f6a-105">Bu öğreticide SignalR hub'larında bağımlılık ekleme yapmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-105">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="d8f6a-106">Ayrıca SignalR ile IOC kapsayıcıları kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-106">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="d8f6a-107">IOC kapsayıcı için bağımlılık ekleme genel bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-107">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="d8f6a-108">Bağımlılık ekleme nedir?</span><span class="sxs-lookup"><span data-stu-id="d8f6a-108">What is Dependency Injection?</span></span>

<span data-ttu-id="d8f6a-109">Zaten bağımlılık ekleme hakkında bilginiz varsa, bu bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-109">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="d8f6a-110">*Bağımlılık ekleme* (dı) olan bir desen burada nesneler kendi bağımlılıklar oluşturmaktan sorumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-110">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="d8f6a-111">DI becerisiyle basit bir örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-111">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="d8f6a-112">İletilerini günlüğe kaydetmek için gereken bir nesne olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-112">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="d8f6a-113">Günlüğe kaydetme arabirimi tanımlayabilir:</span><span class="sxs-lookup"><span data-stu-id="d8f6a-113">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="d8f6a-114">Nesnesi içinde oluşturduğunuz bir `ILogger` iletilerini günlüğe kaydetmek için:</span><span class="sxs-lookup"><span data-stu-id="d8f6a-114">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="d8f6a-115">Bu çalışır, ancak en iyi tasarım değil.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-115">This works, but it's not the best design.</span></span> <span data-ttu-id="d8f6a-116">Değiştirmek istiyorsanız `FileLogger` diğeriyle `ILogger` uygulama, değiştirme gerekir `SomeComponent`.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-116">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="d8f6a-117">Diğer birçok kullanım nesnelerini kabul ederek şehirler `FileLogger`, bunların tümünün değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-117">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="d8f6a-118">Veya yapmaya karar verirseniz `FileLogger` tek Ayrıca uygulama boyunca değişiklik yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-118">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="d8f6a-119">Daha iyi bir yaklaşım "" bulunmaktır bir `ILogger` nesnesine — Örneğin, bir oluşturucu bağımsız değişkenini kullanarak tarafından:</span><span class="sxs-lookup"><span data-stu-id="d8f6a-119">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="d8f6a-120">Nesne seçmek için sorumlu değildir. Şimdi `ILogger` kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-120">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="d8f6a-121">Geçiş yapabilirsiniz `ILogger` bağımlı nesneleri değiştirmeden uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-121">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="d8f6a-122">Bu düzeni olarak adlandırılır [Oluşturucu ekleme](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span><span class="sxs-lookup"><span data-stu-id="d8f6a-122">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="d8f6a-123">Başka bir ayarlayıcı eklemesi, ayarlayıcı yöntemi veya özelliği aracılığıyla bağımlılık ayarladığınız modelidir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-123">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="d8f6a-124">Signalr'da basit bağımlılık ekleme</span><span class="sxs-lookup"><span data-stu-id="d8f6a-124">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="d8f6a-125">Sohbet uygulaması Öğreticisi göz önünde bulundurun [SignalR ile çalışmaya başlama](../getting-started/tutorial-getting-started-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="d8f6a-125">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="d8f6a-126">Bu uygulama hub sınıfı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d8f6a-126">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="d8f6a-127">Sohbet iletileri göndermeden önce sunucuda depolamak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-127">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="d8f6a-128">Bu işlev soyutlayan bir arabirim tanımlayın ve arabirimine eklemesine DI kullanmak `ChatHub` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-128">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="d8f6a-129">Bir SignalR uygulama doğrudan hub'ları oluşturmaz yalnızca sorunudur; SignalR bunları sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-129">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="d8f6a-130">Varsayılan olarak, bir hub sınıfı, parametresiz bir oluşturucu sağlamak için SignalR bekliyor.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-130">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="d8f6a-131">Ancak, kolayca hub örnekleri oluşturmak için bir işlev kaydetmek ve DI gerçekleştirmek için bu işlevi kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-131">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="d8f6a-132">İşlevini çağırarak kaydetmek **GlobalHost.DependencyResolver.Register**.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-132">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="d8f6a-133">SignalR oluşturmanız gerektiğinde bu anonim işlev çağıracağı artık bir `ChatHub` örneği.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-133">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="d8f6a-134">IOC kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="d8f6a-134">IoC Containers</span></span>

<span data-ttu-id="d8f6a-135">Önceki kod, basit durumlar için uygundur.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-135">The previous code is fine for simple cases.</span></span> <span data-ttu-id="d8f6a-136">Ancak yine de bu yazmanız gerekirdi:</span><span class="sxs-lookup"><span data-stu-id="d8f6a-136">But you still had to write this:</span></span>

[!code-css[Main](dependency-injection/samples/sample8.css)]

<span data-ttu-id="d8f6a-137">Birçok bağımlılıkları olan karmaşık bir uygulamada bu "bağlantı" kod yazmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-137">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="d8f6a-138">Bu kod, özellikle bağımlılıkları iç içe geçmişse sağlamak zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-138">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="d8f6a-139">Ayrıca, birim testi de zordur.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-139">It is also hard to unit test.</span></span>

<span data-ttu-id="d8f6a-140">Tek bir çözüm IOC kapsayıcı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-140">One solution is to use an IoC container.</span></span> <span data-ttu-id="d8f6a-141">IOC kapsayıcı bağımlılıkları yönetmekten sorumlu olan bir yazılım bileşenidir. Türleri ile kapsayıcı kayıt ve sonra da kapsayıcı nesneleri oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-141">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="d8f6a-142">Kapsayıcı bağımlılık ilişkileri otomatik olarak belirler.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-142">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="d8f6a-143">Çok sayıda IOC kapsayıcı nesne yaşam süresi ve kapsamı gibi denetlemenize izin.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-143">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="d8f6a-144">"IoC" anlamına gelir "tersine çevirme denetimi için", burada bir çerçeve koduna çağrı genel düzen olduğu.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-144">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="d8f6a-145">IOC kapsayıcı nesnelerinizi sizin için "Normal denetim akışını tersine çevirir" oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-145">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>


## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="d8f6a-146">SignalR öğesinde IOC kapsayıcıları kullanma</span><span class="sxs-lookup"><span data-stu-id="d8f6a-146">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="d8f6a-147">Sohbet uygulaması büyük olasılıkla bir IOC kapsayıcısından yararlanmak basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-147">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="d8f6a-148">Bunun yerine, göz atalım [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) örnek.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-148">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="d8f6a-149">StockTicker örnek iki ana sınıf tanımlar:</span><span class="sxs-lookup"><span data-stu-id="d8f6a-149">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="d8f6a-150">`StockTickerHub`: Hub sınıfına istemci bağlantıları yönetir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-150">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="d8f6a-151">`StockTicker`: Hisse senedi fiyatlarına tutar ve bunları düzenli aralıklarla güncelleştiren bir tekli.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-151">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="d8f6a-152">`StockTickerHub` bir başvuru tutan `StockTicker` tekil, ancak `StockTicker` bir başvuru tutan **IHubConnectionContext** için `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-152">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="d8f6a-153">Bu arabirim ile iletişim kurmak için kullandığı `StockTickerHub` örnekleri.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-153">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="d8f6a-154">(Daha fazla bilgi için [ASP.NET SignalR ile sunucu yayını](index.md).)</span><span class="sxs-lookup"><span data-stu-id="d8f6a-154">(For more information, see [Server Broadcast with ASP.NET SignalR](index.md).)</span></span>

<span data-ttu-id="d8f6a-155">Bu bağımlılıklar biraz ayrıştırmaya IOC kapsayıcı kullanabiliriz.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-155">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="d8f6a-156">İlk olarak, şimdi basitleştirmek `StockTickerHub` ve `StockTicker` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-156">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="d8f6a-157">Aşağıdaki kodda, ihtiyaç duymayacağımız olduğunu miyim bölümlerini açıklamalı.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-157">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="d8f6a-158">Parametresiz oluşturucusu öğesinden kaldırmak `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-158">Remove the parameterless constructor from `StockTicker`.</span></span> <span data-ttu-id="d8f6a-159">Bunun yerine, her zaman DI hub'ı oluşturmak için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-159">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="d8f6a-160">StockTicker için tekil örneğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-160">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="d8f6a-161">Daha sonra IOC StockTicker ömrünü denetlemek için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-161">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="d8f6a-162">Ayrıca, ortak oluşturucu olun.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-162">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="d8f6a-163">Ardından, biz kodu için bir arabirim oluşturarak yeniden düzenleyebilirsiniz `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-163">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="d8f6a-164">Bu arabirim ayrıştırmak için kullanacağız `StockTickerHub` gelen `StockTicker` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-164">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="d8f6a-165">Visual Studio bu kolay tür yeniden düzenleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-165">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="d8f6a-166">StockTicker.cs dosyasını açın, sağ `StockTicker` sınıf bildiriminin ve seçin **yeniden düzenleme** ... **Ayıklama arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-166">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="d8f6a-167">İçinde **Arabirimi Ayıkla** iletişim kutusunda, tıklayın **Tümünü Seç**.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-167">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="d8f6a-168">Diğer varsayılan değerleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-168">Leave the other defaults.</span></span> <span data-ttu-id="d8f6a-169">**Tamam**'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-169">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="d8f6a-170">Visual Studio adlı yeni bir arabirim oluşturur `IStockTicker`ve ayrıca değiştirir `StockTicker` türetmek için `IStockTicker`.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-170">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="d8f6a-171">IStockTicker.cs dosyasını açın ve değiştirmek için arabirimi **genel**.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-171">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="d8f6a-172">İçinde `StockTickerHub` sınıfı, iki örneğinden birini değiştirmek `StockTicker` için `IStockTicker`:</span><span class="sxs-lookup"><span data-stu-id="d8f6a-172">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="d8f6a-173">Oluşturma bir `IStockTicker` arabirimi kesinlikle gerekli değildir, ancak DI uygulamanızın bileşenleri arasında eşleştirme yapmaktan azaltmak için nasıl yardımcı olabileceğini gösteren istedi.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-173">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="d8f6a-174">Ninject kitaplığı Ekle</span><span class="sxs-lookup"><span data-stu-id="d8f6a-174">Add the Ninject Library</span></span>

<span data-ttu-id="d8f6a-175">.NET için çok sayıda açık kaynaklı IOC kapsayıcı vardır.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-175">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="d8f6a-176">Bu öğretici için kullanacağım [Ninject](http://www.ninject.org/).</span><span class="sxs-lookup"><span data-stu-id="d8f6a-176">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="d8f6a-177">(Diğer popüler kitaplıkları içerir [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), ve [StructureMap ](http://docs.structuremap.net).)</span><span class="sxs-lookup"><span data-stu-id="d8f6a-177">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="d8f6a-178">Yüklemek için NuGet Paket Yöneticisi'ni kullanın [Ninject Kitaplığı](https://nuget.org/packages/Ninject/3.0.1.10).</span><span class="sxs-lookup"><span data-stu-id="d8f6a-178">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="d8f6a-179">Visual Studio'da gelen **Araçları** menüsünü seçin **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-179">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="d8f6a-180">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="d8f6a-180">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="d8f6a-181">SignalR bağımlılık çözümleyiciyi değiştirin</span><span class="sxs-lookup"><span data-stu-id="d8f6a-181">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="d8f6a-182">SignalR içinde Ninject kullanmak için türetilen bir sınıf oluşturma **DefaultDependencyResolver**.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-182">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="d8f6a-183">Bu sınıf geçersiz kılmalar **GetService** ve **GetServices** yöntemlerinin **DefaultDependencyResolver**.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-183">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="d8f6a-184">SignalR hub örneklerinin yanı sıra, SignalR tarafından dahili olarak kullanılan çeşitli Hizmetleri dahil olmak üzere çalışma zamanında, çeşitli nesneleri oluşturmak için bu yöntemleri çağırır.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-184">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="d8f6a-185">**GetService** yöntemi, bir türün tek bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-185">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="d8f6a-186">Bu yöntemin Ninject çekirdek 's çağırmaya **TryGet** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-186">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="d8f6a-187">Bu yöntem null değeri döndürür, varsayılan çözümleyici için geri döner.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-187">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="d8f6a-188">**GetServices** yöntemi, belirtilen bir türün nesnelerinin bir koleksiyonunu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-188">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="d8f6a-189">Ninject sonuçlardan varsayılan çözümleyici sonuçları ile birleştirmek için bu yöntemi yok sayın.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-189">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="d8f6a-190">Ninject bağlamaları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d8f6a-190">Configure Ninject Bindings</span></span>

<span data-ttu-id="d8f6a-191">Artık türü bağlamaları bildirmek için Ninject kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-191">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="d8f6a-192">RegisterHubs.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-192">Open the file RegisterHubs.cs.</span></span> <span data-ttu-id="d8f6a-193">İçinde `RegisterHubs.Start` yöntemi çağıran Ninject Ninject kapsayıcı oluşturma *çekirdek*.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-193">In the `RegisterHubs.Start` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="d8f6a-194">Bizim özel bağımlılık Çözümleyicisi örneği oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d8f6a-194">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="d8f6a-195">İçin bir bağlama oluşturun `IStockTicker` gibi:</span><span class="sxs-lookup"><span data-stu-id="d8f6a-195">Create a binding for `IStockTicker` as follows:</span></span>

[!code-html[Main](dependency-injection/samples/sample17.html)]

<span data-ttu-id="d8f6a-196">Bu kod, iki şey diyor.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-196">This code is saying two things.</span></span> <span data-ttu-id="d8f6a-197">İlki, uygulamayı gerektiğinde bir `IStockTicker`, çekirdek örneğini oluşturmalısınız `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-197">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="d8f6a-198">İkinci olarak, `StockTicker` sınıfı tekil nesnesi olarak oluşturulmuş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-198">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="d8f6a-199">Ninject nesnesinin bir kopyasını oluşturmak ve her istek için aynı örnek döndürülecektir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-199">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="d8f6a-200">İçin bir bağlama oluşturun **IHubConnectionContext** gibi:</span><span class="sxs-lookup"><span data-stu-id="d8f6a-200">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="d8f6a-201">Bu kod döndüren anonim bir işlev oluşturur ve bir **IHubConnection**.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-201">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="d8f6a-202">**WhenInjectedInto** yöntemi yalnızca oluştururken bu işlevi kullanmak için Ninject söyler `IStockTicker` örnekleri.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-202">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="d8f6a-203">SignalR oluşturduğu nedeni **IHubConnectionContext** dahili olarak, örnekler ve SignalR bunları nasıl oluşturduğunu geçersiz kılmak istemiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-203">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="d8f6a-204">Bu işlevi yalnızca uygular bizim `StockTicker` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-204">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="d8f6a-205">Bağımlılık çözümleyiciyi içine geçirmek **MapHubs** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="d8f6a-205">Pass the dependency resolver into the **MapHubs** method:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="d8f6a-206">SignalR belirtilen çözümleyici kullanacağı artık **MapHubs**, yerine varsayılan çözümleyici.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-206">Now SignalR will use the resolver specified in **MapHubs**, instead of the default resolver.</span></span>

<span data-ttu-id="d8f6a-207">İçin tam kodu işte `RegisterHubs.Start`.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-207">Here is the complete code listing for `RegisterHubs.Start`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="d8f6a-208">Visual Studio'da StockTicker uygulamayı çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-208">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="d8f6a-209">Tarayıcı penceresinde gidin `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-209">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="d8f6a-210">Uygulamayı önce olarak tam olarak aynı işlevlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-210">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="d8f6a-211">(Bir açıklaması için bkz. [ASP.NET SignalR ile sunucu yayını](index.md).) Davranışı değiştirdik henüz; yalnızca kod sınamak için korumak ve geliştirmek daha kolay.</span><span class="sxs-lookup"><span data-stu-id="d8f6a-211">(For a description, see [Server Broadcast with ASP.NET SignalR](index.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
